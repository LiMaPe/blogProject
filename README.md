<b>#Blog project</b>

This blog project is a part of the Front End Web Developer Nanodegree at Udacity. This project has no starter code and is conducted independently. This project required me to utilize HTML and CSS skills to build out a responsive, multi-device, blog website, including custom images, layout, and styling. Below is first a overview of the subjects covered in this part of the course and later some words on my thoughts and decisions throughout the project.

<b>Part 1. Course overview</b>

The blog project is the end of a series of lectures and exercises in the following subjects with examples of what the lectures covered:

<em>HTML</em>
- Fundamentals of HTML, e.g. elements, attributes, the DOM etc. 
- Separate concerns

<em>CSS</em>
- Fundamentals of CSS, e.g. selectors and linking CSS, display and positioning.
- Specificity
- The Box Model

<em>CSS Flexbox</em>
- Align and distribute content with flexbox in CSS. 
- Fundamental concepts e.g. axes, direction, ordering elements, aligning Items and justify content.

<em>CSS Grid</em>
- Fundamental concepts e.g. rows and columns
- Grid Areas
- Advanced Grid

<em>Creating Responsive Layouts</em>
- Building layouts with Grid
- Media Queries and multiple breakpoints
- Responsive layouts with Grid and Flexbox
- Nesting Grids and making image galleries

<b>Part 2. About the design and process of making this project</b>

<em>Intro</em>

When starting this project I had never made a website with the main focus being on HTML and CSS. I have earlier focused on JS and React, there have of course been HTML and CSS in those aswell but not as the focus subject. 

I needed some inspiration to get going and decided to take a local shop, with nice images on their FB but no website, as my pretend customer. 

<b>Step 1. Mock Pages</b>

My first step was to draw out some mock pages of the website. Here I drew 3 different overviews, for small, medium and large viewports.

<b>Step 2. Building out the HTML for the main page</b>

My first issue what with the naming. I did some research on naming conventions and decided that BEM would be a good choice. I like it because it keeps the CSS flat, meaning it use class name selectors only. This will make problems with specificity far less and styling and debugging easier. In BEM you also want to eliminate dependency on other blocks/elements on a page. I like this as it remind me of parts of React, thinking in components and making the code reusable.  

I decided to finish the main page and it´s styling before moving on the the blog page etc. 

<em>The main page has the following pattern:</em>

1. Header
  - Navbar
  - Social media sharing
2. Power-words 
3. Blog Post Card Gallery
  - Card
  - Image
  - Buttons
4. Contact
  - Link
5. Footer
  - Social media sharing

The part that required the most thought and styling is the blog post card gallery, for this reason I have documented it below so that you can form and better understanding of the process and decisions I made while creating the gallery and the cards. 

<b>Step 3. Styling the main page with CSS.</b>


<em>Page Layout</em>

The page layout is created with Grid. As you can see I use both nested Flexbox and Grid in the page, my take on when to use flexbox and when to use Grid is as follows.

I use Flexbox to make the content flow. Since Flexbox is a single dimensional layout, it is possible to make the content flow in column or rows, but not both. This is where Grid come in. I use to place the content, for example Grid is great for the main page layout, I then nest Flexbox or Grid inside the main Grid depending on what content is going in that Grid area.  


<em>Mobile First</em>

I´ve designed the blogsite using Mobile First, meaning designing for mobile before designing for larger devices. This will make the page display faster on smaller devices and is the recommended standard in this udacity course.

The design changes when the width gets larger, I choose to have three breakpoints. Unfortunately, there are no magic breakpoints due to so many devices, screens, etc. My approach on choosing the @media rules for this design was to base them on the design, that is I gradually narrowed the desktop browser window to observe the natural breakpoints to make sure the design flows nicely on different widths. 


<em>Typography</em>

Contrast

I have made sure to not use a text color with similar color as the background with a too weak contrast.  

Font-size

I wanted a font size that didn´t require me to adjust it for different viewport sizes, that is I want to keep the media queries to a minimum and not include font size. I have only used absolute units before, e.g. px and pt. Relative length units that are commonly used in the examples I´ve seen are the following: em (relative to the font-size of the element), rem (relative to font-size of the root element) and vw and vh (relative to 1% of the width resp. height of the viewport).

For this design I decided to try vw and vh in combination with em to make font sizes that adjust to the width of your screen. The font size will have a base of em and then the responsive part is built by adding vw to it. That is em + vw. By adjusting how many em we start with you make the base smaller or bigger. By adjusting how many vw to add you choose how responsive the text will be, that is a large number will make the text very large on very large screens. 

Read more here: https://css-tricks.com/molten-leading-css/


<em>The Gallery of cards</em>

I decided to show the blogposts as cards on the main page. When creating the cards my first decision was how to create the skeleton, or markup, of the cards. The choice stood between to use a DIV or a UL, I have seen examples of both. 

There is no functional difference between using a DIV vs a UL but I choose to use a UL for the reason that it is the more semantically correct approach. A gallery of cards can be regarded an unordered list, ul, and each card a list item, li. I had the same approach when I created the navigation bar.

Main take away:

  -	Avoid excessive use of div elements
  -	The use of more semantically sound elements makes it easier to read code, and enables you to build CSS definitions with less overhead.

Small screen

For a small screen I wanted a single column of cards. By default flexbox will try to fit all items into one line. To accomplish the column layout I set the flex-direction to column and flex-wrap to wrap. The result is flex items, i.e. the blogpost cards, will wrap onto multiple lines, from top to bottom.

Medium screen

For a medium screen I wanted two column and two rows of cards. I set the flex property to flex: 1 1 43%, This set the flex basis to 43 %, making the cards go 2 by two.  The flex basis defines the default size of an element before the remaining space is distributed. In this case each card gets 43%.

The flex shrink 1 allows the item to shrink to its minimum when there is not enough space. The flex grow 1 will allow the item to grow if there is extra space. The combination makes the cards fully flexible so that they absorb any extra space along the main axis or shrink when needed. 

I choose to set the overflow property to scroll, this will make the text-content available but might be a little distracting. Other options I considered are hide the overflow, add “…“ to the end and to fade out the last line.  Since the amount of text vary between different blog-post card I choose to set the height property to make them even and then deal with the overflow. A different approach would be to target the flexbox properties instead, an nice example I found is here: https://mono.software/2020/07/29/equal-height-cards-with-flexbox/ 

Large screen and Extra-large screen

For larger screens I choose a single row of four cards. This is done by adjusting the flexbasis, in this case 20 % is adequate. Large and Extra-large are similar but with small tweeks to the padding and margins. 


<em>Individual Cards</em>

Each card is made up of three separate items: an image, a text container and a button. 

Image

I wanted the image to be responsive and not come out of proportion. I also wanted it to cover the full width of card. Therefor the width is set to 100 % and the image object-fit property to cover. The image will zoom in and out, leaving different amounts of the edges outside the image but this does not matter in this case. If it would have been e.g. a portrait another solution would have been better, we would not want a headless portrait or a missing neck.

Text

The text is wrapped in a flex container. The flex-direction is set to column making the header com first and the body follow below. 

Button

I want to stretch the button so that it takes up the full width of the card, this is done by setting the width to 100 %. 

<b>File structure</b>

I originally set up a separate CSS file corresponding to each HTML file, but since I was able to reuse most of the main page CSS on each page I decided to refactor and use only one CSS file. The About page for example is only nine lines of unique CSS. This way I don´t have to repeat the code for every page. 








