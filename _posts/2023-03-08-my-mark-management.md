---
layout: post
title: "My Mark Management"
permalink: /my-mark-management
---

I implemented two desktop applications using Kotlin and JavaFX to track course data as assignments for my User Interfaces course. I also built an Android version for the same course, see [My Mobile Mark Management](my-mobile-mark-management).

## Features
The app consists of a toolbar at the top, a scrollable course list, and a status bar at the bottom with stats about the displayed courses. The layout responds to changes in the window size.
<video width="100%" controls autoplay muted loop>
  <source src="assets/mark-management/overview.mp4" type="video/mp4" />
</video>

The top row of the toolbar allows the user to sort and filter the courses in the list. The status bar will update to reflect what's currently being displayed.
<video width="100%" controls autoplay muted loop>
  <source src="assets/mark-management/sort-filter.mp4" type="video/mp4" />
</video>

The user can add new courses using the bottom row of the toolbar. All mandatory fields must be filled in and inputs are validated as needed, for example, course codes must be unique. 

After adding a new course, the course list and status bar will update based on the sorting and filtering criteria. If the filter doesn't allow the new course to be displayed, nothing in the UI will change.
<video width="100%" controls autoplay muted loop>
  <source src="assets/mark-management/add.mp4" type="video/mp4" />
</video>

In the course list, all course fields aside from the code are editable and changes are saved using the update button, which is only enabled once an edit is made. During editing, the delete button turns into a undo button, which reverts any unsaved changes.

The background color for each course entry depends on the grade and will update accordingly if the grade is changed to a different range.

The delete button permanently removes the course.
<video width="100%" controls autoplay muted loop>
  <source src="assets/mark-management/edit-delete.mp4" type="video/mp4" />
</video>

## Spinoff: My Mark Visualization

The next assignment was to extend the previous app by adding an analytics display. Just like in the previous app, the course list is scrollable and allows the user to add, edit, and delete courses. 
<video width="100%" controls autoplay muted loop>
  <source src="assets/mark-visualization/add-edit-delete.mp4" type="video/mp4" />
</video>

The user can click through the tabs in the visualization section to view different graphs. The graphs respond to changes in the window size and the course list. Unfortunately, I couldn't capture window size changes without the footage lagging but the video still shows how the graph scales appropriately for full screen.
<video width="100%" controls autoplay muted loop>
  <source src="assets/mark-visualization/graphs.mp4" type="video/mp4" />
</video>

Average by Term: Displays the average for each term. If no courses were taken that term, the column is left blank.

Progress towards Degree: Displays the number of passed courses and how many are needed to graduate.

Course Outcomes: Groups courses based on the grade. Hovering over a segment shows the courses in the top-left. The checkbox shows the proportion of missing courses that are needed to graduate.

Incremental Average: Displays the cumulative average, the population standard deviation, and the marks of all courses taken up to and including the current term. If no courses were taken that term, the column is left blank.

## Architecture

Both apps use the Model-View-Controller (MVC) design pattern. When the user adds a course, the following steps occur:
1. The user clicks the Create button in the View, sending the input to the Controller. 
2. The Controller tells the Model to add the course.
3. The Model notifies the View that there's been an update.
4. The View refetches the course data from the Model and redraws the graphs.
