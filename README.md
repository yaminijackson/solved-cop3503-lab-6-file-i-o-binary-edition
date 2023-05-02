Download Link: https://assignmentchef.com/product/solved-cop3503-lab-6-file-i-o-binary-edition
<br>
<h1>Overview</h1>

In this assignment, you are going to load a series of files containing data and then searching the loaded data for specific criteria (This sounds oddly familiar…). The files that you load will contain information about various hero characters, some of their attributes (i.e. strength, hit-points, etc.) as well as any items they may be carrying. The data that you load will also be in a <strong>binary format</strong>, which needs to be handled <em>differently</em> than <strong>text-based files</strong>.

<h2>Description</h2>

First things first, the files, there are 2 main files that you will be loading in this assignment:

<ul>

 <li><em>dat </em></li>

 <li><em>dat </em></li>

</ul>

There is a sample file included with this lab document, which you can use to test your code. The file is called <em>SAMPLE_heroes.dat</em>.

The data you are loading is information about the heroes. In binary files, you have to know the format or pattern of the data in order to read it, as you can’t open the file up in a text editor to see what’s in it. (Well, you CAN, but… it won’t be pretty.)

<h1>Hero Data</h1>

The output for a hero would look something like this:




The hero has:

<ul>

 <li>A name</li>

 <li><em>Three</em> attributes stored as <em>short</em> variables</li>

 <li>Hitpoints / Max-hitpoints variables stored as <em>integers</em></li>

 <li><em>Two</em> armor attributes stored as <em>floats</em> from 0-1 (but represented as a <strong>percentage</strong>)</li>

 <li>An inventory containing a variable number of items, each of which contain a <em>name</em>, <em>integer</em> cost, and <em>float</em> for the weight. If a hero doesn’t have any items, the file will still have to indicate a 0. Output-wise, you can just print out</li>

</ul>

“<strong>Inventory empty.</strong>”

<h2>Reading binary data</h2>

Reading data in binary is all about copying <em>bytes</em> (1 byte := 2 nibbles := 8 bits) from a location in a file to a location in memory. When reading data you will <strong>always</strong> use the <em>read()</em> function, and when <strong>writing</strong> data you will always use the <em>write()</em> function. <strong>For this assignment</strong>, you will only need to <em>read()</em> data.

Strings are always an exceptional case. In the case of strings, you should read them in a 4 or 5 step process:

<ol>

 <li>Read the length of the string from the file. Unless you are dealing with fixed-length strings (in which case you know the length of the string from somewhere else), it will be <em>there</em>, promise. (If someone didn’t write this data out to a file, shame on them, they screwed up.)</li>

 <li>Dynamically allocate an array equal to the size of the string, plus 1 for the null terminator. If the length already includes the null terminator, <strong>do not</strong> add one to the count here — you’d be accounting for it twice, which is bad.</li>

 <li>Read the string into your newly created buffer.</li>

 <li>(<strong><u>OPTIONAL</u></strong>) Store your dynamic char * in something like a std::string, which manages its own internal memory. Then you don’t have to worry about it anymore.</li>

 <li>Delete the dynamically allocated array. If you did step 4, this should be immediately after you store it in the std::string (so you don’t forget to delete it later). If you are planning to use this variable later, be sure to delete it later on down the line.</li>

</ol>

Refer back to the Powerpoint slides about Binary File I/O for information on how to read and write binary files.

<h1>File format</h1>

The structure of the files is as follows:

<table width="623">

 <tbody>

  <tr>

   <td width="138">4 bytes</td>

   <td width="486">A <em>count</em> of how many characters are in the file</td>

  </tr>

  <tr>

   <td colspan="2" width="623">“Count” number of characters follow the first 4 bytes. Each character is as follows:</td>

  </tr>

  <tr>

   <td width="138">4 bytes</td>

   <td width="486">The <em>length</em> of the <em>name</em>, including the null terminator</td>

  </tr>

  <tr>

   <td width="138">“Length” bytes</td>

   <td width="486">The string data for the name, including the null terminator</td>

  </tr>

  <tr>

   <td width="138">2 bytes</td>

   <td width="486">The character’s <em>strength</em></td>

  </tr>

  <tr>

   <td width="138">2 bytes</td>

   <td width="486">The character’s <em>intelligence</em></td>

  </tr>

  <tr>

   <td width="138">2 bytes</td>

   <td width="486">The character’s <em>agility</em></td>

  </tr>

  <tr>

   <td width="138">4 bytes</td>

   <td width="486">The character’s <em>current hitpoints</em></td>

  </tr>

  <tr>

   <td width="138">4 bytes</td>

   <td width="486">The character’s <em>maximum hitpoints</em></td>

  </tr>

  <tr>

   <td width="138">4 bytes</td>

   <td width="486">A float representing the character’s <em>physical armor</em> a percentage from 0-1.</td>

  </tr>

  <tr>

   <td width="138">4 bytes</td>

   <td width="486">A float representing the character’s <em>magical armor</em> a percentage from 0-1.</td>

  </tr>

  <tr>

   <td width="138">4 bytes</td>

   <td width="486">A <em>count</em> representing the number of items in the character’s inventory</td>

  </tr>

  <tr>

   <td colspan="2" width="623">“Count” number of Items follow the previous 4 bytes. Each Item is as follows:</td>

  </tr>

  <tr>

   <td width="138">4 bytes</td>

   <td width="486">The length of the string representing the <em>name</em> of the item, including the null terminator</td>

  </tr>

  <tr>

   <td width="138">“Length” bytes</td>

   <td width="486">The string <em>data</em> for the name of the item, including the null terminator</td>

  </tr>

  <tr>

   <td width="138">4 bytes</td>

   <td width="486">The value of the item (in gold pieces, diamonds, gil, gems, dollars, whatever currency you want to imagine for this project)</td>

  </tr>

  <tr>

   <td width="138">4 bytes</td>

   <td width="486">A <em>floating-point</em> number for the weight of the item</td>

  </tr>

 </tbody>

</table>

<strong> </strong>




<h2>Searches</h2>

After you’ve loaded the data, you will do a few searches on your heroes:

<ol>

 <li>Print all the heroes</li>

 <li>Print the hero with the most items</li>

 <li>Who’s the strongest?</li>

 <li>Who has an intelligence greater than 18?</li>

 <li>Who are the 2 clumsiest heroes (lowest and second-lowest agility)?</li>

 <li>Which hero has the most valuable inventory?</li>

</ol>

<h2>Sample outputs</h2>




Strongest hero




2 clumsiest heroes




Hero with the most valuable stuff (Superman the hoarder!)




<h1>Tips</h1>

<ol>

 <li>Choices you make at the start of a program can have a big impact on how the rest of the program gets developed. Think about how you want to store the information retrieved from the file, and how you could easily pass that data to various functions you might write.</li>

 <li>If you have a process for easily loading and accessing the data, the rest of the functionality should be a lot easier to write. Make sure the loading process is all taken care of before worrying about anything else.</li>

 <li>The code to load 1 file containing 1 piece of data (no matter how complex that data is) should not be much different than loading 100 files, each containing 100 elements. Start by thinking about just 1 element from the file first. Do the values you read match the values in the file? What about 2 entries, does everything add up? Then 3, 4, etc…</li>

 <li>When passing containers of data, make sure you pass them by REFERENCE, not by value. Creating copies of massive data sets is generally a bad, bad thing… unless you specifically need to duplicate the data. If not? Then pass by reference (in C++ that means either by pointer or the reference data type)</li>

 <li>There may be a fair amount of repetition in a program like this. Think about where you can create helper functions to reduce the number of times you write the exact same (or just slightly different) code.</li>

 <li>Boy these tips seem familiar. It’s almost like there’s a lot of similarity between this and things you’ve done before… use this to your advantage, now and in the future.</li>

 <li>Try reading one element at a time. Read the first 4 bytes, try printing it out to the screen. Is the number something reasonable, or something that seems incorrect, like -20? If that works, move on to the next piece of data in the file.</li>

</ol>