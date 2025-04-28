# FlexibleMessageBox for .NET WinForms (C#)

A flexible, single-file replacement for the standard .NET `System.Windows.Forms.MessageBox`, enhanced with Rich Text Format (RTF) support, improved auto-sizing, and modern C# features.

Based on the original work by Jörg Reichert, with modifications and updates.

## Features

* **Drop-in Replacement:** Designed to be used similarly to the standard `MessageBox`, supporting common `Show()` method overloads.
* **Single File:** Easy integration into any WinForms project by adding just one `.cs` file.
* **Resizable:** Users can resize the message box window.
* **Word Wrapping:** Content is automatically word-wrapped.
* **Rich Text Format (RTF) Support:** Display messages with rich formatting (bold, italics, colors, etc.) using the `ShowRtf()` methods.
* **Improved Auto-Sizing:** Intelligently calculates the optimal size to fit the content (both plain text and RTF), respecting maximum width/height constraints relative to the screen's working area.
* **Hyperlink Support:** Automatically detects and enables hyperlinks within the message text.
* **Icon Support:** Displays standard `MessageBoxIcon` types (Information, Warning, Error, Question).
* **Button Customization:** Supports standard `MessageBoxButtons` combinations (OK, OKCancel, YesNo, YesNoCancel, AbortRetryIgnore, RetryCancel).
* **Default Button:** Specify the button that should have initial focus.
* **Localization:** Includes button text translations for English, German, Spanish, and Italian.
* **Keyboard Shortcuts:** Supports standard MessageBox keyboard interactions (Ctrl+C/Ctrl+Insert to copy, Escape to close/cancel).
* **Configurable:** Adjust maximum size factors and the default font.
* **Modernized Code:** Updated to leverage newer C# language features for clarity and conciseness.

## How to Use

1.  **Add the File:** Add the `FlexibleMessageBox.cs` file to your WinForms project.
2.  **Call `Show()` or `ShowRtf()`:** Use the static methods just like you would with the standard `MessageBox`.

### Basic Examples (Plain Text)

```csharp
using JR.Utils.GUI.Forms;
using System.Windows.Forms;

// Simplest usage
FlexibleMessageBox.Show("This is a simple message.");

// With caption
FlexibleMessageBox.Show("Operation completed successfully.", "Success");

// With caption, buttons, and icon
DialogResult result = FlexibleMessageBox.Show(
    "Are you sure you want to proceed?",
    "Confirmation",
    MessageBoxButtons.YesNo,
    MessageBoxIcon.Question);

if (result == DialogResult.Yes)
{
    // User clicked Yes
}

// Specifying owner and default button
FlexibleMessageBox.Show(
    this, // Owner window
    "An error occurred: File not found.",
    "Error",
    MessageBoxButtons.OK,
    MessageBoxIcon.Error,
    MessageBoxDefaultButton.Button1); // Button1 corresponds to the first button (e.g., OK)


RTF Examples
using JR.Utils.GUI.Forms;
using System.Windows.Forms;

// Simple RTF message
string rtfContent = @"{\rtf1\ansi{\fonttbl\f0 Arial;}\f0\pard This is \b bold\b0, this is \i italic\i0.}";
FlexibleMessageBox.ShowRtf(rtfContent, "RTF Example");

// RTF with color and different fonts (ensure fonts are installed)
string complexRtf = @"{\rtf1\ansi\deff0{\fonttbl{\f0 Arial;}{\f1 Times New Roman;}{\f2 Courier New;}}
{\colortbl ;\red0\green0\blue255;\red255\green0\blue0;}
\pard\f0\fs24 This is default text (Arial 12pt).\par
\f1\fs28 This is Times New Roman 14pt.\par
\f2\fs20 This is Courier New 10pt.\par
This is \cf1 blue\cf0 , and this is \cf2 red\cf0.\par
\b Bold\b0 , \i Italic\i0, \ul Underlined\ulnone .\par
}";
FlexibleMessageBox.ShowRtf(complexRtf, "Complex RTF", MessageBoxButtons.OK, MessageBoxIcon.Information);

// RTF with a link (links are automatically detected in both plain text and RTF)
string rtfWithLink = @"{\rtf1\ansi\pard Visit our website: {\field{\*\fldinst{HYPERLINK ""[http://www.example.com](http://www.example.com)""}}{\fldrslt{[www.example.com](https://www.example.com)}}}} for more info.\par}";
// Or simply include the URL in the RTF string, RichTextBox often auto-detects.
string simpleLinkRtf = @"{\rtf1\ansi\pard Check [www.google.com](https://www.google.com) \par}";
FlexibleMessageBox.ShowRtf(simpleLinkRtf, "Link Example");



Configuration
You can modify the static properties of the FlexibleMessageBox class before calling any Show methods, typically during application startup:
// Set the maximum width to 50% of the screen's working area
FlexibleMessageBox.MAX_WIDTH_FACTOR = 0.5;

// Set the maximum height to 80% of the screen's working area
FlexibleMessageBox.MAX_HEIGHT_FACTOR = 0.8;

// Set a custom font for the message box
FlexibleMessageBox.FONT = new Font("Segoe UI", 10f);


License
This software is based on the original work by Jörg Reichert, published at CodeProject. The original license statement is included below:
THE SOFTWARE IS PROVIDED BY THE AUTHOR "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OF THIS SOFTWARE.
Please refer to the original CodeProject article for more details: http://www.codeproject.com/Articles/601900/FlexibleMessageBox
Credits
Original Author: Jörg Reichert (public@jreichert.de)
Original Contributors: David Hall, Roink
RTF & Modernization Modifications: Chris Pringle
Feel free to adapt and extend this code
