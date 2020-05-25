<!--
---
title: UI Manifesto
tags: [ui,manifesto,best practice,error handling,animations,transitions,responsive design]
link: https://github.com/monstar-lab-group/ui-manifesto
---
-->

# UI Manifesto

Normally designs are delivered as frozen versions of an interactive app. This document tries to outline some of the gaps in a static design file in Zeplin and specs out what is the baseline for a great app.

In each section there is a _Do_ and _Do not_ list to highlight some of the things to be aware of and what to avoid doing.

Table of Contents
=================
 * [Loading](#loading)
    * [Loading in general](#loading-in-general)
    * [Form loading](#form-loading)
    * [Searching](#searching)
    * [Pull to refresh](#pull-to-refresh)
 * [Empty state/views](#empty-state-views)
 * [Error handling](#error-handling)
    * [No connection](#no-connection)
    * [Failed loading the view - no data to show](#failed-loading-the-view-no-data-to-show)
    * [Failed to refresh list or content](#failed-to-refresh-list-or-content)
    * [No content/search result error](#no-content-search-result-error)
    * [Form validation](#form-validation)
    * [Background error](#background-error)
    * [Login token expired](#login-token-expired)
 * [Transitions](#transitions)
 * [Animations](#animations)
 * [Responsive design](#responsive-design)


## Loading

### Loading in general

When the app is waiting on the API

| Do                                                                                        | Do not                                                                                | 
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| Disable buttons that can interfere with an ongoing action | Avoid blocking navigation when loading, the user should be able to "cancel" actions in case of timeouts or similar |
| Always provide button states, so the user is aware that buttons are disabled |  |

### Form loading

When the app takes input and sends input to API such as a login or settings screen.

| Do                                                                                        | Do not                                                                                | 
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| Disable all input fields or hide them while waiting for a response | Overlay the input fields with a loader |
| Disable buttons while loading so only one request is sent  | Overlay the input fields with a loader |
| Hide the keyboard | |


### Searching

When the app takes search strings and maybe provides autocomplete

| Do                                                                                        | Do not                                                                                | 
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| Limit searches to at least 2 characters or more | Start searching immediately |
| Debounce/throttle searches to once every 2 seconds or so, this will easy the API load, but also simplify client state | Send a request for every character written |
| Cancel any outbound request when starting a new search, so we avoid response A being received after response B  | Overlay the input fields with a loader |
| Show a loader whenever a request is in flight, so the user is aware of incoming results | Only show results without a loader, the user will potentially misclick when the results switches |

### Pull to refresh

When a list is reloading content. **We should always implement pull to refresh in lists with changing data.**

| Do                                                                                        | Do not                                                                                | 
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| Use platform standards so the behaviour is familiar to the user | Implement an additional blocking loader if pull to refresh is available. Programmatically show the pull to refresh loader if manual refresh is being done |
| Merge/diff results so the list is partly updated or even animated with changes |  |


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
| Explain what the requirements for the fields are, or what is wrong with the current input | Clear the input fields if a field is invalid                                          |
| Submit button is disabled/hidden until all required fields are valid. Guide the user to fix errors in the space where the button will be. | Clear the input field when entering an input field again                              |
| If there's more than one error, consider adding a summary at the bottom of the form, to let the user know where the errors are |                                                                                       |
| If validation can only be done on submit, a non-invasive loading spinner should be shown until the data has been validated and errors should be shown as stated above.         |                                                                                       | 
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
| Show error page explaining that its time to log in again, for security reasons (Consider this being an overlay or popup to keep the user in a familiar setting)            | Open on the sign-in page                                                              |
| Button to sign in again (Goes to the standard login screen)                               | Stay in the app and show loading errors                                               |

## Transitions

## Animations

## Responsive design

