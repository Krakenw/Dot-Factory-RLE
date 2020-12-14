# Dot-Factory-RLE


This RLE version of the Dot Factory–EXE was generated with Visual C# Express-8
On windows XP, and requires Microsoft .NET Framework to be installed. 
.NET  version 3.5 was tested and found to be OK on XP service pack 3.

The source for this RLE version is included in the zip file.

This file and the exe could use some improvement. So if you want to make changes
please do so.

On the ‘Modify output configuration’ window under the Spanner Icon. You will
Find an extra dropdown list, which contains the RLE output options.

 

The program / application “The Dot Factory” is an excellent tool for producing
Bit-Mapped Fonts from existing True-Type fonts.

Bit-Mapped Fonts are often used with micro-controllers and LCD screen projects.

One of the drawbacks of “large fonts” when used in the Bit-Mapped format is the large amount 
of memory they consume, which is usually in short supply on micro-controllers.

The use of Run-Length-Encoded “RLE” fonts helps reduce the storage size of the larger 
fonts. Small fonts used with RLE will often take up more storage memory.


The implementation of RLE used to generate fonts in this program is very simple,
And yet quite effective. The program generates an array of bytes that represent the
font characters in a similar way to an ordinary bitmapped font array. However
The array is “hopefully” smaller than the bitmapped array and is interpreted differently. 

Also some other smaller arrays are used to hold the width of each character and possibly 
the encoding type (Horizontal or Vertical) and another possibly holding the offset into 
the font array for each character. Some of these arrays could be stored together sharing 
the bits of a single byte. 

This depends on how you store the Font in your language and application, and the maximum 
width of a characters used.

And lastly you will require the height of the font, which should be the same for all characters.

It is assumed that your project will contain and LCD controller, and that you can tell
The controller to set-up a rectangle on the LCD for writing to, of a size and shape 
corresponding to the font character that you want to render to the screen. 

It is also assumed that the pixel writing will always start at the top left hand corner of the rectangle.

If the font character was encoded Horizontally:- 
pixel writing will continue writing a line left to right then moving to the next row down, again 
writing a line left to right until writing ends at the bottom right hand corner. 

If the font character was encoded Vertically:- 
pixel  writing will continue writing a column Top to Bottom then moving to the next column on the 
right again writing Top to Bottom until writing ends at the bottom right hand corner. 


Now all we need to know is whether to write a Foreground pixel or Background pixel at each write location 
and this is where the RLE array comes in to play.

Each byte in the RLE array describes whether to write a Foreground or Background colour and how many pixels 
to write in that colour, all pixels described by the byte will be the same colour. 

The MSB (Most Significant Bit) signifies the pixel colour:
0 = Background Colour.
1 = Foreground Colour. 
 (Your own code supplies the actual pixel colour)

The lower 7 bits depict how many pixels to write.
1-127 pixels – It will never be zero in this particular RLE implementation.

(With hindsight it should have been the (7 bit value + 1) for best compression)

If the font was encoded using Vertical & Horizontal encoding for better compression
It will be necessary flip the “writing direction bit” in the LCD controller each time the
font characters vertical or  horizontal encoding changes.

For best compression all characters should be encoded with no excess white space
at the sides of each character. This makes the font automatically variable width and you will 
responsible for adding white space between each character. All characters will have the same 
height made up of white space at the top or bottom or both.

(You can still generate fixed width fonts if required)

Hopefully you will find some example code snippets showing some C++ implementations of font classes and RLE pixel decoding & rendering.









  











