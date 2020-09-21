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
 * [Authentication](#authentication)
 * [Data entry](#data-entry)
 * [Loading](#loading)
    * [Loading in general](#loading-in-general)
    * [Form loading](#form-loading)
    * [Searching](#searching)
    * [Pull to refresh](#pull-to-refresh)
 * [Empty state and views](#empty-state-and-views)
 * [Error handling](#error-handling)
    * [No connection](#no-connection)
    * [Failed loading the view due to no data to show](#failed-loading-the-view-due-to-no-data-to-show)
    * [Failed to refresh list or content](#failed-to-refresh-list-or-content)
    * [No content due to search result error](#no-content-due-to-search-result-error)
    * [Form validation](#form-validation)
    * [Background error](#background-error)
    * [Login token expired](#login-token-expired)
 * [Transitions](#transitions)
 * [Animations](#animations)
 * [Audio](#audio)
 * [Responsive design](#responsive-design)
 * [Accessibility](#accessibility)

## Authentication
| Do                                                                             | Do not                                                                                    |
|--------------------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| Support biometric authentication when possible                                | Ask for both password and biometry in the same login flow to authenticate the user |
| Reference authentication methods accurately based on the device’s capabilities | Reference Face ID on devices that support only Touch ID, and the other way around  |
| Handle the scenario of biometry being disabled by the users                    |                                                                                          |
| Provide password auto fill functionality                                       |                                                                                          |

## Data entry
| Do                                                                                                                                                                            | Don't                                                        |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| Provide a list of predefined options to speed up the process when possible                                                                                                    | Make fields required if it's not really neccesary      |
| Provide an easy way to navigate thought lists of options, for example sort the lists alphabetically or in another logical matter that can speed up the selection for the user |                                                              |
| Provide hints and placeholders to help communicate the purpose                                                                                                                |                                                              |
| Provide reasonable default values                                                                                                                                             |                                                              |
| Enable buttons to continue only after all required data is entered                                                                                                            |                                                              |
| Use enabled/disabled buttons as a cue that the user can proceed                                                                                                               |                                                              |
| Dynamically validate fields, when possible check values immediately so users can correct them right away                                                                      |                                                              |
| Provide the appropriate keyboards based on the data needed (Alphabet, Numeric, Email, etc.)                                                                                   |                                                              |
| Dismiss keyboards when tapping outside the field                                                                                                                              |                                                              |

## Loading

### Loading in general

When the app is waiting on the API

| Do                                                                                                                        | Do not                                                                                                              |
|---------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| Disable buttons that can interfere with an ongoing action                                                                 | Avoid blocking navigation when loading, the user should be able to "cancel" actions in case of timeouts or similar |
| Always provide button states, so the user is aware that buttons are disabled                                              |                                                                                                                    |
| Make it clear when the loading is occurring                                                                               |                                                                                                                    |
| Show activity spinners or skeleton views when the content is loading                                                      |                                                                                                                    |
| If the loading time is longer, provide progress, like for example file uploads                                            |                                                                                                                    |
| Do not make the users wait for content to load before seeing the screen, show the screen immediately with a loading state |                                                                                                                    |                                   |       |

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


## Empty state and views
| Do                                                                                                                                                   | Don't                                                                                          |
|------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|
| Show clear and short information about why there is no data                                                                                          | Leave empty spaces in the view where there is a section with no data, adapt your screens |
| Give the users hints on what they can do to see data as some views will depend on user actions                                                       | Show error state for empty state                                                         |
| Add scroll views when the design might not fit smaller devices                                                                                       | Present an blank view                                                                    |
| Adhere to safe areas and other system layout guidelines                                                                                              |                                                                                                |
| If possible, support both portrait and landscape orientations                                                                                        |                                                                                                |
| Have a clear agreement between backend and frontend developers of what data can be missing and how will that be represented in the backend responses |                                                                                                |
| If a view is composed of multiple sections, make sure that the view looks good even if parts of data are missing                                     |                                                                                                |

## Error handling

### No connection

When the app does not have an internet connection.

| Do                                                                                        | Do not                                                                                | 
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| A non-invasive error message, toast, or snack bar. (“No connection”)                      | Block the UI with an error overlay                                                    |
| If it blocks what the user is doing, show a dialog with an explanation                    | Clear existing data                                                                   |
|                                                                                           | Present a blank view                                                                  |
|                                                                                           | Present an empty state view                                                           | 

### Failed loading the view due to no data to show

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

### No content due to search result error

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
| Do                                                        | Do not |
|-----------------------------------------------------------|-------|
| Use native transitions                                    |       |
| Only use custom transitions if specified by designers     |       |
| Keep transitions consistent for views with same behaviour |       |

## Animations
| Do                                                               | Do not                                                                                                     |
|------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| Add subtle animations only if they provide a benefit to the user | Use animations just for the sake of animations. Excessive and out of place animations can distract the users. |
| Keep the animation styles consistent across the app              |                                                                                                               |
| Strive to use the built in animations of the platform            |                                                                                                               |

## Audio
| Do                                                           | Do not                                          |
|--------------------------------------------------------------|-------------------------------------------------|
| Use sounds effects in the app only if specified by designers | Add non essential sounds effects to apps |

## Responsive design
| Do                                                             | Don't |
|----------------------------------------------------------------|-------|
| Develop your screens with responsiveness in mind               |       |
| Preview your app on multiple devices                           |       |
| Add scroll views when the design might not fit smaller devices |       |
| Adhere to safe areas and other system layout guidelines        |       |
| If possible, support both portrait and landscape orientations  |       |

## Accessibility
| Do                                                                            | Don't |
|-------------------------------------------------------------------------------|-------|
| Provide ample touch targets for interactive elements                          |       |
| If you use animations, make them optional to give the option to reduce motion |       |
| Provide dark mode support                                                     |       |
| Provide support for dynamic type sizes                                        |       |
