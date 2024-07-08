# Designing Fonts

---

## Font Size: Choosing a Scale

-   Smaller jumps is okay for bottom sizes, but not for upper sizes
-   Use modular scale, such 4:5 (major third), 2:3 (perfect fifth), or 1:1.618 (golden scale)
    -   Although its not perfect in practical, such as (1) ending up with fractional sizes, (2) usually need more font size
-   Use hand-crafted scale. Here that work well on most project: 12px, 14px, 16px, 18px, 20px, 24px, 30px, 36px, 48px, 60px, 72px
-   Avoid em units!



## Font Family: Use Good Fonts

-   Play it safe. For UI design, stick to neutral sans-serif (e.g., Helvetica). Or stick to system font stack
-   Ignore typefaces with less than 5 weight.
    -   10+ weights if accounting italics. Typefaces with many weights usually crafted with care
-   Optimize for legibility
    -   For headlines, use tighter letter-spacing & shorter x-height.
    -   For smaller text, use wider letter-spacing & taller x-height.
    -   Avoid using condensed typefaces with short x-height.
-   Trust the wisdom of crowd. Popular typefaces probably is a good fonts.
-   Steal from people who cares. Check and use "Inspect" => "Styles" => "font-family: ..."



## Line Length: Keep Line Length in Check

When styling paragraph, you may try to fit the text into layout. **Its a mistake and making the lines that too long, making text harder to read**.

-   When styling paragraph, avoid making lines that too long
    -   For best reading experience, make the paragraph wide enough to fit 45 and 75 characters per line. Easiest way is using *em* units. Width of 20-35 *em* is convenient.
    -   Going wider than 75 characters per line can work, but its a risky territory. Stick to 45-75 for playing safe.
-   Dealing with wider content. When you're mixing paragraph with other large component, you should still keep the line length in check. Above rule apply.



## Line Height: Line Height is Proportional

-   **Accounting for paragraph width**. It means that line height and paragraph width should be proportional. The more longer the paragraph, the more bigger the line height.
    -   Narrow content can use shorter line-height (e.g., 1.5), while wider content might need to be taller (e.g., 2)
-   **Accounting for font size**. Means that line-height and font size is also proportional. But its has *inverse proportional*
    -   **When text is small, you need bigger line-height** (e.g., 16px font size, with 2 line-height on wide lines)
    -   **When text is big, such as headlines, you not need extra line-height**. (e.g., 48px font size, with 1 line-height)



## Text Alignment: Baseline,  Not Center

-   A situation where you need different font size to create hierarchy might occur. In that case, you may vertically align (i.e., `align-items: center;`) the text.
-   A better approach is to align mixed font sizes by their baseline, an imaginary line that letters rest on.



## Color: Not Every Link need Color

-   When you include a link in a non-link text, its important to make it stands out and looks clickable. Such as changing color to blue with underline, in a wall of non-text with black color.
-   But, when you designing an interface where almost everything is a link, don't make it appear "popped out". Instead, emphasize it in subtle way.
    -   For example, Youtube interface is all link. Use heavier font weight or darker color (e.g., title of video)
    -   Some link not need to be emphasized. Simply give it underline or changing color only on hover (e.g., channel name in video's card)



## Align with Readability in Mind

-   Don't center long form text.
    -   Center-alignment can looks great for headlines or short-independent block of text.
    -   But for longer than two or three lines, don't center them. It'll almost always looks good left-align
    -   If you still want center-align, make it shorter
-   Right-align number
-   Hyphenate justified text. Justified text may works great in print or web, but it can incur awkward gaps between words.
    -   Always enable hyphenation on justified text, that is `hyphens: auto;` or `hyphens: manual;`
    -   Justified text works best in situations where you're try to mimic a print look. Even then, left-aligned text works great too.



## Letter Spacing: Use Effectively

-   As general rule, it better to trust the typeface designer and leave letter-spacing alone.
-   There may be situation where adjusting letter-spacing can improve design. When designer create typefaces, they designed it with purpose in mind. A family such **"Open Sans" designed to be legible at small sizes**, so **it has wider letter-spacing** than, for example, **"Oswald" that designed for headlines**.
    -   **Tightening headlines where the family has wide letter-spacing** may become a right decision.
    -   Avoid trying to make it work the other way (i.e., headlines fonts rarely work for small text)
-   Improving all-caps legibility.
    -   Letter-spacing **in most typefaces usually optimized for normal sentence** - a capital followed by mostly lowercase letter
    -   Lowercase letter have more variety, such that fit entirely within baseline and x-height (e.g., n, e, v), that has ascender (e.g., b, f, t), or that has descender (e.g., y, g, p).
    -   All-caps text, on the other hand, isn't so diverse. Since every letter has same height and use same spacing often leads to harder-to-read text. ==Because of that, its make sense to increase letter-spacing for all-caps text== such giving `0.05 em` spacing.



---

# Wrapping Up

```markdown

```











