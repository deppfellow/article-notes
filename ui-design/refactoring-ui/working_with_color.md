# 1. Use HSL

..Instead of RGB or HEX. HSL has better representation attributes to human-eye: *hue*, *saturation*,  and *lightness*:

-   **Hue** is the color's position in color wheel
-   **Saturation** is how vivid the color is. 0 is grey (i.e. no color) and 100 is vibrant (i.e. full color)
-   **Lightness** measure how close the color is to white or black. 0 is pure black while 100 is pure white. 50 is pure color at given hue.



# 2. Need More Color

You can't really build anything with only five hex color. To do that, break a good color palette down into three categories:

-   **Greys**. Almost everything in interface is greys.
    -   You need plenty of greys, 8-10 shades. Start with dark grey as true black looks unnatural.
-   **Primary color(s)**. These determines the primary actions, active navigation elements, etc.
    -   You need one, or sometime two. Each with 5-10 shades.
    -   Ultra-light shades useful for tinted-colored background for things such alerts.
    -   Darker shades work great for text.
-   **Accent colors**. Few of it to communicating different things to user.
    -   For example, eye-grabbing color such yellow, pink, or teal to highlight new features. Red for destructive. Yellow for warning. Green for positive trend.
    -   Use sparingly throughout the UI

As a rule of thumbs, 60% of elements should use the main color, 30% should use secondary (i.e. main accents) color, and 10% for other accent colors (e.g. for destructive, warning, info, etc).



# 3. Define Shades Up Front

How to to it?

1.  **Choose the base color first**. 

    The middle where the light and dark shades will be based on. A good rule of thumb is to pick a shade that work well as a button background.

2.  **Finding the edges**

    Pick the darkest and lightest shades. The darkest shades usually reserved for text, while the lightest shades might be used for background of element.

3.  **Filling in the gaps**

    After getting the darkest 900, base 500, and lightest 100, start fill gaps between them. Start from value of 700 and 300 until you satisfied. Then fill the rest.

The same for greys. Pick the edges then fill in the gap.



# 4. Lightness Kill Saturation

In HSL color space, as color closer to the edges, the impact of saturation weakened. It means that **if you don't want the color look washed out** as lightness nearing toward 0 or 100, **we need to increase saturation**. This is become important when the color is applied to large section of UI.



# 5. Use Perceived Brightness

![workWithColor-innateBrightness](.\img\workWithColor-innateBrightness.png)

Which of these two color look lighter. Although "yellow" seems lighter, it turn out both has same lightness value. And thing to know, every hue has its inherent perceived brightness due to human eye nature. You can calculate the perceived brightness of color by plug its RGB component into below:
$$
\frac{\sqrt{0.299 \cdot r^2 + 0.587 \cdot g^2 + 0.114 \cdot b^2}}{255}
$$
<img src=".\img\workWithColor-brightnessGraph.png" alt="workWithColor-innateBrightness" style="zoom:67%;" />



# 6. Change Brightness with Hue

Its certainly an interesting thing to understand, but thing get more interesting when you realize you can use it to designs.

**Normally when you change how light color looks, you adjust the *lightness* component**. While this work to lighten or darken a color, you often lose color's *intensity* as the color just look more white or black.

Since different hues have different perceived brightness, we can change it brightness by rotating its *hue*:

-   **To make color lighter**, rotate *hue* towards nearest bright hue ー 60, 180, or 300 degree.
-   **To make color darker**, rotate *hue* towards nearest dark hue ー 0, 120, or 240 degree.
-   **Don't rotate more than 20-30 degree** as it will make its like a different color, rather than more light or dark.

This can also be used to create color palette, as for example, it make base color yellow looks more orangish as you decrease the lightness. The darker shade feels more warm & rich rather than dull & brown.



# 7. Saturated Greys

By definition, true grey has saturation of 0, meaning it doesn't have actual color at all. But in practice, a lot of colors that we think greys is saturated quite heavily. It what make a grey feels cool while the other feel warm.

## Color temperature

Just like blue feel cooler and yellow feel warmer, saturating grey works the same.  If you want grey feel cool, saturate them with a bit of blue. If you want greys feel warmer, saturate with a bit of yellow or orange.

<img src=".\img\workWithColor-saturatingGreys.jpg" alt="workWithColor-saturatingGreys" style="zoom: 80%;" />

To maintain consistent temperature, also increase saturation for lighter and darker shades. If not, it'll make the grey looks washed out, just like previously explained that lightness kill saturation. How much saturation is up to you.



# 8. Accessible Design

To make your design accessible, Web Content Accessibility Guidelines (WCAG) recommend normal text (i.e. under ~18px) has contrast ratio of at least 4.5:1, while larger text has 3:1, based on their background color.

When working with dark-text-on-light-background, this is pretty easy. Thing get tricky when start working with color.

-   **Flipping the contrast**
    -   When working with white text on colored background, it'd be hard to meet those 4.5:1 ratio. Darkening the background may cause hierarchy issue as dark background will grab user attention. 
    -   To deal with that, flip the contrast by **use the dark text on lighter-colored background**.
-   **Rotating the hue**
    -   What harder than white text on colored background is colored text on colored background. You might encounter this when try to use a a color for secondary text inside dark-colored text.
    -   To deal with that, remember that some color are brighter than others. So to increase the contrast without getting the text closer to white is **by rotating the hue towards brighter color**, such cyan, magenta, or yellow.



# 9. Don't Rely on Color Alone

Color can be useful to communicating information, but color-blind people may have hard time to interpret. Easy fix is to **also communicate with other element, such icons**. 

*On graph* where each portion have different color, **use contrast to differing between light and dark**.





# Personal Note: Wrapping Up

-   In designing, use HSL color instead of RGB or HEX
-   You'll need a lot, but limited, of color. Prepare at least a primary color, secondary color, 3-5 accents color, and greys.
-   For each colors, prepare 9-11 shades. First choose the middle (i.e. 500 value), define the edges (i.e. 100 and 900 values), then start fill the gap between them.
-   By increasing lightness, it make color washed out and not vibrant. So as lightness nearing 0 or 100, from value of 50, increase the saturation at the same time.
-   Each hue has its own *innate brightness*. Use at your advantage...
-   ...so rather than adjusting saturation and lightness to change brightness, rotate the hue instead:
    -   To lightening, rotate to nearest 60, 120, 180 degree
    -   To darkening, rotate to nearest 0, 120, 240
    -   Don't rotate more than 20-30 degree. It'll make it like totally different color.
-   Rather than using pure grey (i.e. 0 saturation), try to give them temperature by using blue and yellow/orange color. Giving it a little saturation based on whether to make it cooler or warmer, respectively.
-   Maintain good contrast ratio between text-color and background-color.
    -   In case of white text on colored background, try flipping the contrast. Swap the background-color to lighter and text-color to darker.
    -   In case of colored text on colored background, try rotating the hue of the text to brighter color.