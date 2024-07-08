# Figma Basics

## Aligning Object

Aligning Object based on position and axis

-   **Alt + [A, D, W, S]** for align left, right, top, and bottom respectively
-   **Alt + [H, V]** for align horizontal or vertical, respectively

Distributing object

-   **Alt + Shift + [H, V]** for distributing spaces in horizonal or vertical, respectively.
-   **Ctrl + Alt + Shift + T** for tidy up (i.e., distribute both horizontal and vertical)



## Layers: Frame, Groups, and Section

-   <u>Frames</u> serve as fundamental, accommodate everything screen layouts to components. Ideal for:
    -   Screen & component design, different layout of mobile, tablet, desktop. Serve as container
    -   Component creation, for creating reusable design elements such buttons, icons, or input fields
    -   Grids & layouts, apply layout grids to maintain consistent spacing and alignment.
-   <u>Groups</u> ideal for quick, temporary arrangement. Used to keep component's spacing in place when used with alignment.
-   <u>Sections</u> ideal for enhancing collaboration. streamline navigation, and presentation. Have mark button that say ready for development for designer telling developer that the design is ready.



## Selecting & Inspecting

To select all component that has same properties, fill, stroke, etc in the same frames, use:

-   Upper left figma icon => Edit =>  "Select all with ..."

To select the underlying frames without needing to click at the frame's name, use:

-   Ctrl + click on frame



## Constraints

Constraints used to adjust element inside frames to scales, shift, or stay in place. It can keep the padding, spacing, and alignment of elements insides stay still, making the frames looks responsive.

-   Types of constraints
    -   Top/Left to keep elements' spacing stays from top or left of the frame
    -   Bottom/Right to keep elements' spacing stays from bottom or right of the frame
    -   Left and Right/Top and Bottom to keep elements' spacing stays from left-right or top-bottom, at the same time.
    -   Center to keep element stays center as the frame resized
    -   Scale to keep element scales proportionally as the frame resized



---

# Layouts

## Layout Grids

Using layout grid to align elements to a grid system. Pair really well with constraint. [Usual grid system ](https://bootcamp.uxdesign.cc/12-8-4-column-system-for-responsive-grids-df207a58ebc)for overall layout is:

-   Desktop (Large 1440+ dp, medium 1240-1439 dp, medium 905-1239 dp)
    -   12 columns
    -   Center type
    -   72px width, auto margin, and 24px gutter
-   Tablet (Medium 600-904 dp)
    -   8 columns
    -   Stretch type
    -   Auto width, auto/24px margin, 24px gutter
-   Mobile (Small 0-599 dp)
    -   4 columns
    -   Stretch type
    -   Auto width, 16px margin, 16px gutter

Other than that, we can use grid layout to make custom grid such as 3 rows, for header, content, and footer section. Then align columns for overall layout as needed.



## Auto Layout

Can be seen similar to flexbox. 

-   Shift + A, to make frame into auto layout
-   Alt + Shift + A, to remove auto layout into frame
-   Double click on edge, to set hug contents
-   Alt + double click on edge, to set fill container



---

# Styles, Typography, and Variables

## Styles & Typography

-   Placeholder



## Variables

Variables, just like coding, store specific and reusable values. It can be color codes, font sizes, spacing measurement, etc. These variables then can be applied to properties of different Figma elements. We can create color palette with variables in fast way using plugin: **"variables2css"**.

Usually, variables used with tokenization:

-   Global token (1st tier token), define the general variables
-   Semantic token (2nd tier token), define the used token such primary, secondary, danger, warning, etc
-   Component token (3rd tier token), define the used token for each component element (e.g., button token)

Because variables can only store one variable, its usually preferred to use styles to create component token since component token frequently has specific value.



---

# Components

Components used to create a reusable elements. First, create the element, then "**Ctrl + Alt + K**" to create component from an element

## Component Properties

