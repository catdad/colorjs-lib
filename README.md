# ColorJS

So you want to convert and calculate colors in JavaScript? You've come to the right place.

[Click here for the live demo here](http://catdad.github.io/ColorJS).

##How to use

In the browser:

    <script src="http//catdad.github.io/tiny.cdn/lib/colorjs/latest/color.min.js"></script>
    
In Node.js:

    var Color = require('colorjs-lib');
    
_Note: npm is coming soon._

##Create

Simple create methods

    Color("#ff0000");
    Color({r:255,g:0,b:0});
  
Advanced create methods

    Color.fromHEX("#ff0000");
    Color.fromRGB({r:255,g:0,b:0});
    Color.fromRGBA({r:255,g:0,b:0,a:.5});
    Color.fromArray([255,0,0]);
    Color.fromRYB({r:255,y:0,b:0})
  
Under advanced methods, there are also options to create colors from `HEX`, `RGB`, `RGBA`, `CMYK`, `HSV`, `HSL`, and `RYB`, using an `Object` or `Array` values. There is also a random color generator.

    Color.fromCMYK({c: 0, m: 1, y: 1, k: 0});
    Color.fromCMYK([0, 1, 1, 0]);
    
    Color.fromHSV({h: 0, s: 1, v: 1})
    Color.fromHSL({h: 0, s: 1, l: 0.5});
    
    Color.random();
  
##Getters and Setters

Once you have created a color, you can convert it to any format you would like, as such:

    var color = Color("#ff0000");
  
    color.HEX(); //"ff0000"
    color.CSS(); //"#ff0000"
    color.RGB(); //{r: 255, g: 0, b: 0}
    color.HSV(); //{h: 0, s: 1, v: 1}
    color.HSL(); //{h: 0, s: 1, l: 0.5}
    color.CMYK(); //{c: 0, m: 1, y: 1, k: 0}
    color.RYB(); //{r: 255, y: 0, b: 0}
    
    color.toString(); //"#ff0000"
    
The same functions can be used to set the color of an existing `Color` object by passing the appropriate value.

    var color = Color("ff0000");
    color.CMYK(); //{c: 0, m: 1, y: 1, k: 0}
    
    color.CMYK({c: 1, m: 1, y: 0, k: 0});
    color.HEX(); //0000ff

##Color scheme calculator

You can use this library to calculate color various named color harmonies.

    //HUE +/- 30 degrees
    color.analog(); //[original, plus, minus]
    
    //HUE +/- 120 degrees
    color.triad(); //[original, plus, minus]
    
    //HUE +/- 150 degrees
    color.split(); //[original, plus, minus]
    
    //HUE + 180 degrees
    color.complement(); //[original, complement]

_Note: These values are mathematical suggestions, and may need to be adjusted slightly to make a more pleasant color combination or remain in the same color gamut._

The tetratic/quadratic color scheme is a special case, in that it takes an offset parameter in degrees. This offset it used to calculate the color scheme rectangle. The default is 40 degrees, which was a subjective choice.

    var offset = 30;
    color.quadrat(offset); //[original, color1, color2, color3]

Calculate any generic (unnamed) three color scheme using the hue shifter function:

    //HUE +/- degrees
    color.hueShift(degrees); //[original, plus, minus]
    
More generic hue shifter, which returns only one value:

    //HUE + degrees
    color.hueShiftSingle(degrees); //newColor

Hue shifts based on how many colors you need, which will calculate colors at equal invervals:

    var count = 5;
    color.contrasts(count); //[original, color1, color2, color3, color4];
    
_Note: This name will likely change, as it is not very intuitive._

_Note: This function obviously has a limit of usefulness, as too many colors will result colors being too close to one another. This is a mathematical limitation, and there isn't much I can do about it. If you need more colors, try calculating this from two (or seven) colors from a different color gamut to get more contrasting colors._

Monochromatic calculations, based on the number of colors you need:

    var count = 3;
    color.monochrome(count); //[color1, color2, color3]
    
Calculate only lighter or darker monochrome colors:

    color.monochromeLight(count); //[original, lighter1, lighter2]
    color.monochromeDark(count); //[original, dark1, dark2]
    
_Note: The monochrome functions does not return pure black or white. Add those on your own if you need to. Also, `monochrome` does not necessarily return the original color, but rather colors of the same hue._

Mix in another color:

    var red = Color('ff0000');
    var cyan = Color('00ffff');
    
    var purple = red.minin(cyan);
    purple.CSS(); // return #aa55aa
    
You can also use the `mix` method on the `Color` object to mix any two colors together:

    var red = Color('ff0000'),
        cyan = Color('00ffff');
    
    var purple = Color.mix(red, cyan);

Mixing colors this way will adjust the new color for lightness, so that it matches the original colors used for the mixture. You can skip the adjustment like this:

    var red = Color('ff0000'),
        cyan = Color('00ffff');
    
    var purple = Color.mix(red, cyan); // #aa55aa
    var darkerPurple = Color.mix({
        color1: red,
        color2: cyan,
        match: false
    }); // #804080
    
Mixing also supports ratios:

    var red = Color('ff0000'),
        cyan = Color('00ffff');
    
    var someSortOfPink = Color.mix({
        color1: red,
        color2: cyan,
        ratio: .7
    }); // #d22d5c

All ratios are first color to second color. You may need to disable matching here, especially if trying to mix with white or black.

##Note

All colors are stored as RGBA values. Some rounding needs to occur for this, especially for HSL and HSV values. This will result in colors being ever so slightly different. If this is unacceptable, please look elsewhere.

##Thanks

Special thanks to my art school girlfriend, who answered all of my incessant questions about color theory. If you would like to read up on it as well, try this article: [Color Theory, The Color Wheel And Color Schemes](http://www.vanseodesign.com/web-design/color-theory/).

Also, thanks to the guys at EasyRGB for their helpful [color math and formulas](http://www.easyrgb.com/index.php?X=MATH).

##License

This project is licensed under the MIT X11 License. Please use, adapt, and modify this project to your heart's content. Link back to this page wherever you can.

[![Analytics](https://ga-beacon.appspot.com/UA-17159207-7/colorjs-lib/readme)](https://github.com/igrigorik/ga-beacon)
