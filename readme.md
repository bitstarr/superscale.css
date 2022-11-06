# superscale.css

What happens to the website when the screen is really big and really high resolution? Your design team shrugs its shoulders and the client complains about the narrow content strip in the whitespace prairie?

Save yourself the discussion, just blow the thing up above FullHD - with **superscale.css**!

## How it works

```css
:root {
    /* super scale! */
    @media ( min-width: 120.01rem ) {
        font-size: calc( 100vw / 120 );
    }
    /* but not for iOS - it's not smart enough */
    @supports (-webkit-touch-callout: none) {
        font-size: 1rem;
    }
}
```

Provided the base font-size of your website is equal to 16px, a FullHD viewport will be 120rem wide and you are using only relative and font based units. To keep scaling proportioanlly, the `:root` font-size will be set to a calculation of a 120th of 100vw after the breakpoint of 120rem. After that point we lock the 1rem unit to this fraction of the viewport size.

## Demo

Look at this [CodePen example](https://codepen.io/bitstarr/full/gOwaNoB).

## Customization

If you want to fix your design earlier or later, you need to modify calculation. For example you want to start scaling at 2240px viewport width (at 1rem=16px), replace 120 with 140. The math is `1920/16 = 120` and `2240/16 = 140`.

## Caveats

This method requires you to use relative units, preferredly font units (rem, em, ex, ch, …) and percentages for basically everything! Every use of pixel units could cause problems.

Also certain browsers (looking at this californian orchard) or the way you work with font-size on the `html` element may cause issues.

I am using this for some years in multiple projects and only ran in a few issues that could be fixed. While testing there were hardly issues when setting a different `body` font size than (equal to) 16px. The media query in `:root` seems to be oriented to the browser setting. If the user sets its default font size to 20px, your scaling may begin earlier than you expect, but assuming the user set this fonts size deliberately, it will encourage accessibilty though.