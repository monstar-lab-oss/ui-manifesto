<!--
---
title: UI Manifesto
tags: [ui,manifesto,best practice,error handling,animations,transitions,responsive design]
link: https://github.com/monstar-lab-group/ui-manifesto
---
-->

# UI Manifesto

TODO: Description of Filling out the gaps of provided designs

Table of Contents
=================
 * [Loading](#loading)
 * [Empty state/views](#empty-state-views)
 * [Error handling](#error-handling)
    * [No connection](#no-connection)
    * [Failed loading the view - no data to show](#failed-loading-the-view-no-data-to-show)
    * [Failed to refresh list or content](#failed-to-refresh-list-or-content)
    * [No content/search result error](#no-content-search-result-error)
    * [Form validation](#form-validation)
    * [Background error](#background-error)
    * [Login token expired](#login-token-expired)
 * [Transitions](#empty-state-views)
 * [Animations](#empty-state-views)
 * [Responsive design](#empty-state-views)


## Loading

## Empty state/views

## Error handling

### No connection

When the app does not have an internet connection.

| Do                                                                                        | Do not                                                                                | 
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| A non-invasive error message, toast, or snack bar. (“No connection”)                      | Block the UI with an error overlay                                                    |
| If it blocks what the user is doing, show a dialog with an explanation                    | Clear existing data                                                                   |
|                                                                                           | Present a blank view                                                                  |
|                                                                                           | Present an empty state view                                                           | 

### Failed loading the view - no data to show

When an entire view can't be loaded.

| Do                                                                                        | Do not                                                                                | 
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| An in-view empty state                                                                    | Present an error dialog                                                               |
| Explain the error in non-technical terms                                                  | Block the UI with an error overlay                                                    |
| "Try again" button                                                                        | Reload without the user initializing the reload attempt                               |
|                                                                                           | Present a blank view                                                                  |


### Failed to refresh list or content

When a list of elements is updating and an error occur.

| Do                                                                                        | Do not                                                                                | 
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| A non-invasive error message, toast or snack bar                                          | Present an error dialog                                                               |
| Or a silent fail if it doesn't affect the user                                            | Block the UI with an error overlay                                                    |
|                                                                                           | Clear existing data in the list                                                       |
|                                                                                           | Present a blank view                                                                  |
|                                                                                           | Present an empty state view                                                           |

### No content/search result error

When there is no content to load.

| Do                                                                                        | Do not                                                                                | 
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| In view empty state                                                                       | Present an error dialog                                                               |
| An explanation that there's no content to show                                            | Block the UI with an error overlay                                                    |
| Explanation of how to add content if this is relevant                                     | Present a "Try again" button                                                          |
|                                                                                           | Present a blank view                                                                  |

### Form validation

When validating input fields.

| Do                                                                                        | Do not                                                                                | 
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| Validate on leaving the input field, not on form submit                                   | Present an error dialog                                                               |
| Present the error at the input field                                                      | Block the UI with an error overlay                                                    |
| Explain what the requirements for the fields are, or what is wrong with the current       | Clear the input fields if a field is invalid                                          |
input                                                                                       | Clear the input field when entering an input field again                              |
| Submit button is disabled/hidden until all required fields are valid. Guide the user 
to fix errors in the space where the button will be.                                        |                                                                                       |
| If there's more than one error, consider adding a summary at the bottom of the form, 
to let the user know where the errors are.                                                  |                                                                                       |
| If validation can only be done on submit, a non-invasive loading spinner should be 
shown until the data has been validated and errors should be shown as stated above.         |                                                                                       | 
### Login error

When an error happens on login (or invalid login credentials).

| Do                                                                                        | Do not                                                                                | 
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| Non-invasive error message (Toast/snack bar/TextView)                                     | Present an error dialog                                                               |
| Highlight input fields if credentials are wrong                                           | Block the UI with an error overlay                                                    |
|                                                                                           | Clear the input fields if a field is invalid                                          |
|                                                                                           | Clear the input field when entering an input field again                              |

### Background error

If an error occurs in the background (i.e. timeout).

| Do                                                                                        | Do not                                                                                | 
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| Do not show if it's not relevant for the user and what they are doing currently.          | Present an error dialog                                                               |
|                                                                                           | Block the UI with an error overlay                                                    |
|                                                                                           | Show a toast or snack bar                                                             |

### Login token expired

If the login token expired and the user opens the app.

| Do                                                                                        | Do not                                                                                | 
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| Show error page explaining that its time to log in again, for security reasons 
(Consider this being an overlay or popup to keep the user in a familiar setting)            | Open on the sign-in page                                                              |
| Button to sign in again (Goes to the standard login screen)                               | Stay in the app and show loading errors                                               |

## Transitions

## Animations

## Responsive design

