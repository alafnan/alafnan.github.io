---
layout: post
title: Project-01 MTA Turnstile Analysis
---


<div style="margin-bottom: 1rem;   padding: 1rem;   color: #FFFFFF;   background-color: #000000; font-family: Arial, Helvetica, sans-serif; font-size:0.9em;">
Group Members: Bader Alafnan, Khaled Al Qahtani, Abdulrahman Alshetwi, Aiman Alghamdi and Abdulrahman Alkhthlan
</div>

<h1 style="font-size:1.5em; color:#000000; margin-top: 2rem; margin-bottom: 1rem;">Project Overview:</h1>

<p style="text-align: justify; text-justify: inter-word;"> WomenTechWomenYes (WTWY) has an annual gala at the beginning of the summer each year. As they are new and inclusive organization, they are trying to do double duty with the gala both to fill our event space with individuals passionate about increasing the participation of women in technology, and to concurrently build awareness and reach.To this end they place street teams at entrances to subway stations. The street teams collect email addresses and those who sign up are sent free tickets to thier gala. Where they like to solicit our engagement is to use MTA subway data, which is available freely from the city, to help them optimize the placement of thier street teams, such that they can gather the most signatures, ideally from those who will attend the gala and contribute to our cause.</p>

<h1 style="font-size:1.5em; color:#000000; margin-top: 2rem; margin-bottom: 1rem;">Project objectives:</h1>

<div style="margin-bottom: 1.2rem; padding: 1rem;   color: #000000;   background-color: #F0EDE5; font-family: Arial, Helvetica, sans-serif; font-size:0.8em; text-align: left;" >
  <ul>
  <li>To help <strong>WomenTechWomensYes</strong> (WTWY) organisation to optimise the placement of thier street teams.</li>
  <li>To provide (WTWY) with <strong>bussiness solutions</strong> to reduce the <strong>cost</strong> of thier advertisment project.</li>
  <li>To provide (WTWY) with the <strong>optimum days</strong> and <strong>times</strong> at top five utilised <strong>stations</strong>.</li> 
  <li>To provide (WTWY) with the optimum <strong>UNITS</strong> inside each of the five stations.</li>
  <li>To provide (WTWY) with a <strong>pi chart</strong> that shows the percentage of utilised stations.</li> </ul> </div>


<h1 style="font-size:1.5em; color:#000000; margin-top: 2rem; margin-bottom: 1rem;">Resources of Data from MTA:</h1>
Click the Link: [Turnstile Data MTA Website](http://web.mta.info/developers/turnstile.html)


<h1 style="font-size:1.5em; color:#000000; margin-top: 2rem; margin-bottom: 1rem;">Project Approach:</h1>
<p style="text-align: justify; text-justify: inter-word;"> The figure below shows the project approach that we followed to make the project work, starting with collecting, understanding, analysing the data and finally give solutions to the organisation. </p>
![Project Approach Image]({{ site.url }}/images/pro1.jpg)

<h1 style="font-size:1.5em; color:#000000; margin-top: 2rem; margin-bottom: 1rem;">Visualising the data:</h1>
<p style="text-align: justify; text-justify: inter-word;"> The data was visualised using <strong>Jupyter Notebook</strong> via Python3 syntax as shown in the figure below. The figure shows the first five rows out of a total of <i>203363</i> rows using the follwoing comman line {% highlight python %}Train.head()      # to read file Train{% endhighlight %} Notice that the data was read from file <strong>turnstile_190511</strong> on MTA website. </p>
![Data]({{ site.url }}/images/pro2.jpg)

<h1 style="font-size:1.5em; color:#000000; margin-top: 2rem; margin-bottom: 1rem;">Important codes for data cleansing:</h1>



{% highlight python %}
# Importing main libraries 
import datetime
import pandas as pd
import collections
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn
import os

# Read the data file
Train = pd.read_csv('turnstile_190511.txt')
# remove spaces if there is space in the columns
Train.columns = [column.strip() for column in list(Train.columns)]
# Shift up one column and substract from the another 
Train['D_ENTRIES'] = Train.ENTRIES.shift(-1)-Train.ENTRIES
Train['D_EXITS'] = Train.EXITS.shift(-1)-Train.EXITS
# git rid of unexpected values by estimating the max and min 
Train = Train[(Train.D_ENTRIES> 0) & (Train.D_ENTRIES < 4000) & 
                (Train.D_EXITS > 0) & (Train.D_EXITS < 4000)]
# convert date and time from str to datetime64
Train['DATE_TIME'] = pd.to_datetime(Train.DATE + Train.TIME, format='%m/%d/%Y%H:%M:%S')
# # Deleting unnecessary files from the data
Train = Train.drop(['DIVISION', 'TIME', 'DESC', 'ENTRIES', 'EXITS'], 1)

{% endhighlight %}

## Inline HTML elements

HTML defines a long list of available inline tags, a complete list of which can be found on the [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).

- **To bold text**, use `<strong>`.
- *To italicize text*, use `<em>`.
- Abbreviations, like <abbr title="HyperText Markup Langage">HTML</abbr> should use `<abbr>`, with an optional `title` attribute for the full phrase.
- Citations, like <cite>&mdash; Mark otto</cite>, should use `<cite>`.
- <del>Deleted</del> text should use `<del>` and <ins>inserted</ins> text should use `<ins>`.
- Superscript <sup>text</sup> uses `<sup>` and subscript <sub>text</sub> uses `<sub>`.

Most of these elements are styled by browsers with few modifications on our part.

## Footnotes

Footnotes are supported as part of the Markdown syntax. Here's one in action. Clicking this number[^fn-sample_footnote] will lead you to a footnote. The syntax looks like:

{% highlight text %}
Clicking this number[^fn-sample_footnote]
{% endhighlight %}

Each footnote needs the `^fn-` prefix and a unique ID to be referenced for the footnoted content. The syntax for that list looks something like this:

{% highlight text %}
[^fn-sample_footnote]: Handy! Now click the return link to go back.
{% endhighlight %}

You can place the footnoted content wherever you like. Markdown parsers should properly place it at the bottom of the post.

## Heading

Vivamus sagittis lacus vel augue rutrum faucibus dolor auctor. Duis mollis, est non commodo luctus, nisi erat porttitor ligula, eget lacinia odio sem nec elit. Morbi leo risus, porta ac consectetur ac, vestibulum at eros.

### Code

Inline code is available with the `<code>` element. Snippets of multiple lines of code are supported through Pygments. Longer lines will automatically scroll horizontally when needed.{% endhighlight %} 

{% highlight js %}
// Example can be run directly in your JavaScript console

// Create a function that takes two arguments and returns the sum of those arguments
var adder = new Function("a", "b", "return a + b");

// Call the function
adder(2, 6);
// > 8
{% endhighlight %}

You may also optionally show code snippets with line numbers. Add `linenos` to the Pygments tags.

{% highlight js linenos %}
// Example can be run directly in your JavaScript console

// Create a function that takes two arguments and returns the sum of those arguments
var adder = new Function("a", "b", "return a + b");

// Call the function
adder(2, 6);
// > 8
{% endhighlight %}

Aenean lacinia bibendum nulla sed consectetur. Etiam porta sem malesuada magna mollis euismod. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa.

### Gists via GitHub Pages

Vestibulum id ligula porta felis euismod semper. Nullam quis risus eget urna mollis ornare vel eu leo. Donec sed odio dui.

{% gist 13f94b734a4ddb132735 gist.md %}

Aenean eu leo quam. Pellentesque ornare sem lacinia quam venenatis vestibulum. Nullam quis risus eget urna mollis ornare vel eu leo. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sed odio dui. Vestibulum id ligula porta felis euismod semper.

### Lists

Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Aenean lacinia bibendum nulla sed consectetur. Etiam porta sem malesuada magna mollis euismod. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa justo sit amet risus.

* Praesent commodo cursus magna, vel scelerisque nisl consectetur et.
* Donec id elit non mi porta gravida at eget metus.
* Nulla vitae elit libero, a pharetra augue.

Donec ullamcorper nulla non metus auctor fringilla. Nulla vitae elit libero, a pharetra augue.

1. Vestibulum id ligula porta felis euismod semper.
2. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.
3. Maecenas sed diam eget risus varius blandit sit amet non magna.

Cras mattis consectetur purus sit amet fermentum. Sed posuere consectetur est at lobortis.

<dl>
  <dt>HyperText Markup Language (HTML)</dt>
  <dd>The language used to describe and define the content of a Web page</dd>

  <dt>Cascading Style Sheets (CSS)</dt>
  <dd>Used to describe the appearance of Web content</dd>

  <dt>JavaScript (JS)</dt>
  <dd>The programming language used to build advanced Web sites and applications</dd>
</dl>

Integer posuere erat a ante venenatis dapibus posuere velit aliquet. Morbi leo risus, porta ac consectetur ac, vestibulum at eros. Nullam quis risus eget urna mollis ornare vel eu leo.

### Images

Quisque consequat sapien eget quam rhoncus, sit amet laoreet diam tempus. Aliquam aliquam metus erat, a pulvinar turpis suscipit at.

![placeholder](http://placehold.it/800x400 "Large example image")
![placeholder](http://placehold.it/400x200 "Medium example image")
![placeholder](http://placehold.it/200x200 "Small example image")

### Tables

Aenean lacinia bibendum nulla sed consectetur. Lorem ipsum dolor sit amet, consectetur adipiscing elit.

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Upvotes</th>
      <th>Downvotes</th>
    </tr>
  </thead>
  <tfoot>
    <tr>
      <td>Totals</td>
      <td>21</td>
      <td>23</td>
    </tr>
  </tfoot>
  <tbody>
    <tr>
      <td>Alice</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <td>Bob</td>
      <td>4</td>
      <td>3</td>
    </tr>
    <tr>
      <td>Charlie</td>
      <td>7</td>
      <td>9</td>
    </tr>
  </tbody>
</table>

Nullam id dolor id nibh ultricies vehicula ut id elit. Sed posuere consectetur est at lobortis. Nullam quis risus eget urna mollis ornare vel eu leo.

-----

Want to see something else added? <a href="https://github.com/poole/poole/issues/new">Open an issue.</a>

[^fn-sample_footnote]: Handy! Now click the return link to go back.
