## Design Token

-   Border radius and width variables
-   Primitive and semantic color variables
-   Spacing variables
-   Layout grids
-   Typography for web, IOS, and Android

---

### Border

#### Border radius

-   Square edge can show seriousness, while round edge can show friendly
-   Naming example:

| Name   | Size |
| ------ | ---- |
| Circle | 50%  |
| Pill   | 999  |
| L      | 16   |
| M      | 12   |
| S      | 8    |
| XS     | 4    |



#### Border width

-   Example, border of input field become thicker when the state change to *focus*

-   Naming example:

| Name | Size |
| ---- | ---- |
| XL   | 8    |
| L    | 4    |
| M    | 2    |
| S    | 1.5  |
| XS   | 1    |



---

### Primitive and Semantic Colors

#### **Primitive colors** 

-   Are the base-line hues, color that you use as the default color for your design. 
-   It has color scale, from tints (lighter) to shades (darker).
-   We do naming to our primitive color with convention "Color (group)/Values", such as "Blue/500".

#### **Semantic colors** 

-   Have meaning and named based on how they're used, not what they look.
-   **Primitive color assigned to semantic color**, and **named based on how they used** for components

<img src=".\img\fds-semantic_color_naming.png" alt="fds-semantic_color_naming" style="zoom: 80%;" />

We use schema below to name our semantic:

| Group                                                     | Role                 | Appearance | State    | Value |
| --------------------------------------------------------- | -------------------- | ---------- | -------- | ----- |
| Text (e.g. text/icon)                                     | Primary              | Bold       | Hover    | L0    |
| Background                                                | Secondary            | Subtle     | Focus    | L1    |
| Border                                                    | Tertiary             | Inverse    | Pressed  | L2    |
| Surface (e.g. elevation, shadow)                          | Brand                |            | Selected | L3    |
| Overlay (e.g. when modal appear and background goes dark) | Mono                 |            | Disabled | L4    |
|                                                           | Link                 |            |          | L5    |
|                                                           | Info                 |            |          | L6    |
|                                                           | Notice/Warning       |            |          | 50    |
|                                                           | Negative/Destructive |            |          |       |
|                                                           | Positive/Success     |            |          |       |

For example...

![fds-semantic_documentation-1](.\img\fds-semantic_documentation-1.png)

![fds-semantic_documentation-2](.\img\fds-semantic_documentation-2.png)

![fds-semantic_documentation-3](.\img\fds-semantic_documentation-3.png)



---

### Spacing

Spacing is space between each interface and components, ensuring readability, visual harmony, and usability.

#### **Scale**

We'll use global 8 point system with t-shirt sizing.

| Size | Multiplier | Value (px) |
| ---- | ---------- | ---------- |
| 12XL | 14         | 112        |
| 11XL | 13         | 104        |
| 10XL | 12         | 96         |
| 9XL  | 11         | 88         |
| 8XL  | 10         | 80         |
| 7XL  | 9          | 72         |
| 6XL  | 8          | 64         |
| 5XL  | 7          | 56         |
| 4XL  | 6          | 48         |
| 3XL  | 5          | 40         |
| 2XL  | 4          | 32         |
| XL   | 3          | 24         |
| L    | 2          | 16         |
| M    | 1.5        | 12         |
| S    | 1          | 8          |
| XS   | 0.5        | 4          |
| 2XS  | 0.24       | 2          |



Example of implementation below:

-   **Component**, in input field below, the label and help text are 8px away from field (i.e. **margin**). Inside field has **padding** of 16px horizontal and 12px vertical. The text and icon are separated by 8px **gap**.

    ![fds-spacing_example-1](D:\any_code\article-notes\ui-design\img\fds-spacing_example-1.png)

-   **Content**, in cards below, the content (i.e. text) is given 16px **padding**, 8px **gap** between *heading* and *text*, and 16px **gap** between *text* and *metadata*.

    ![fds-spacing_example-2](D:\any_code\article-notes\ui-design\img\fds-spacing_example-2.png)

-   Screens, in app below, there is **24px side margins** that keeping the content from edges. Inside the content area, there is **16px gap** between each content blocks. Moreover, there is **8px gap** between heading and text content in each block.

    ![fds-spacing_example-3](D:\any_code\article-notes\ui-design\img\fds-spacing_example-3.png)



---

### Layout and Breakpoints

#### Layout

Usually refer to set of vertical columns that allow designers to define their components in structured way

-   **Desktop and landscaped tablet**: 12 columns

-   **Portrait tablet**: 8 columns

-   **Mobile**: 4 columns

-   **Breakpoints**, is specific points at which interface adapt to accommodate different screen sizes

    -   Different breakpoints example:

        | Device           | Type    | Name | Size |
        | ---------------- | ------- | ---- | ---- |
        | Desktop          | Center  | XL   | 1440 |
        | Tablet Landscape | Stretch | L    | 1024 |
        | Tablet Portrait  | Stretch | M    | 768  |
        | Mobile           | Stretch | S    | 393  |



---

### Typography

Typography is art of arranging type(s) to make written language readable, legible, and visually appealing. It plays in establishing hierarchy of content.

-   Font family

    Setting up typography start with font family. Here is using **Inter** as default type face, **SF Pro Display** and **SF Pro Text** for iOS, and **Roboto** for Android.

-   Weight

    Font family comes in different weight, defining how thick each characters. Frequently use are **Regular** and **Semi-bold**.

    ```markdown
    1. font-thin: 100
    2. font-extralight: 200
    3. font-light: 300
    4. font-normal: 400  <= Frequently used for most text
    5. font-medium: 500  <= Frequently used for most text
    6. font-semibold: 600  <= Frequently used for emphasized text
    7. font-semibold: 700  <= Frequently used for emphasized text
    8. font-extrabold: 800
    9. font-black: 900
    ```

-   Groups

    Two groups that can cover most use cases, **Heading** and **Text**. 

-   Scale

    Using combination of global 4 point scale and t-shirt sizing. Instead of naming them such h1 to h6, body, etc, we use t-shirt sizing naming: from 2XS to 5XL.

| Group   | Size | Weight    |
| ------- | ---- | --------- |
| Heading | 5XL  | Regular   |
| Text    | 4XL  | Semi bold |
|         | 3XL  |           |
|         | 2XL  |           |
|         | XL   |           |
|         | M    |           |
|         | S    |           |
|         | XS   |           |
|         | 2XS  |           |

![fds-typography_documentation-1](.\img\fds-typography_documentation-1.png)

![fds-typography_documentation-2](.\img\fds-typography_documentation-2.png)

