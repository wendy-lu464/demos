---
layout: post
title: "My Mobile Mark Management"
permalink: /my-mobile-mark-management
---

This is an Android app built using Kotlin to track course data. This was built for my User Interfaces course and is based on the desktop app created for the same course, [My Mark Management](my-mark-management).

## Features
The main screen provides a scrollable list of courses, as well as filtering and sorting functions.
<video width="100%" controls autoplay muted loop>
  <source src="assets/mobile-mark-management/main.mp4" type="video/mp4" />
</video>

The user can add, edit, and remove course information. Input validation is applied on the add and edit screens. The course background colour is based on the grade and will change accordingly if the grade is changed to a different range.
<video width="100%" controls autoplay muted loop>
  <source src="assets/mobile-mark-management/add-edit-delete.mp4" type="video/mp4" />
</video>

Toggling the WD (withdraw) switch to the on position will disable user input for the Mark field. Toggling it off will restore the last inputted numerical grade.
<video width="100%" controls autoplay muted loop>
  <source src="assets/mobile-mark-management/wd.mp4" type="video/mp4" />
</video>

The app responds to device orientation changes.
<video width="100%" controls controls autoplay muted loop>
  <source src="assets/mobile-mark-management/turn.mp4" type="video/mp4" />
</video>

## Architecture

This app uses Single-Activity Architecture, a common way to build Android apps. There is one main activity and the user navigates between 3 different Fragments: the Main, Edit, and Add screens.

To store state, the app uses a simplified version of the Model-View-ViewModel (MVVM) design pattern where the Model and ViewModel logic are combined into one ViewModel class.
In a larger application, I would implement a separate class for the Model, but that separation wasn't necessary here.
