# Hiearachy is Everything

Section two of "Refactoring UI" book.

---

***Visual hierarchy*** refer to **how important an elements in an interface appear in relation to one another**. When everything in an interface competing for attention, it'll feels noisy and chaotic. By **de-emphasize secondary and tertiary information**, and making effort to **highlight the element that most important**.

## Size isn't everything

Relying on font size too much is a mistake -- as it'll lead to primary content too large, and secondary content too small.

Instead, **try using font weight or color**. For instance:

-   Making primary element bolder to let us use more reasonable font size
-   Using softer color for secondary text instead of using tiny font, makes it more clear in sacrifice of readability.
    -   Stick to two or three **colors**: A **dark color** for primary (e.g., headline), a **grey** for secondary (e.g., date of article), and a **lighter grey** for tertiary (e.g., copyright notice)
    -   Two **font weight** usually enough for UI work: 400/500 for most text, 600/700 to emphasized text.

![hierarchy-noRelyOnFontSize](.\img\hierarchy-noRelyOnFontSize.png)

!!! **Stay away** from **font weight under 400** for UI work. They are hard to read. If you want to de-emphasize some text, try to use lighter color or smaller font size instead.



## Don't use grey text on colored backgrounds

Making text a lighter grey is great to de-emphasize text on white background, but **not in colored background**. That's because, on white background, we're seeing the effect on white is reduced contrast.

You might think that the easiest way  is to use white text with reduce opacity, but this instead, often result in text that looks dull, washed out, and the worse is when the background has pattern, it'll shown in the text too.

![hierarchy-noTextOnColorBg-Wrong](.\img\hierarchy-noTextOnColorBg-Wrong.png)

The right way is, making text closer to the background is what help create hierarchy. A better approach is to pick a new color, based on the background color. **Choose color with same hue, then adjust the saturation and lightness** until it looks good.

![hierarchy-noTextOnColorBg-Right](.\img\hierarchy-noTextOnColorBg-Right.png)



## Emphasize by de-emphasizing

Sometime we may run into situation where the main element isn't standing out enough, but there's nothing you can add to give it the emphasis that it need. For example, even by giving the active "nav" item its own color, it still doesn't stand out compared to inactive nav.

In these situation, instead of further emphasize the focus element, **try to de-emphasize the other element that it compete with**.

![hierarchy-empByDeemp](.\img\hierarchy-empByDeemp.png)

![hierarchy-empByDeemp-2](.\img\hierarchy-empByDeemp-2.png)



## 