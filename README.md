# Frontend Mentor - Article preview component solution

This is a solution to the [Article preview component challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/article-preview-component-dYBN_pYFT). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
- [Acknowledgments](#acknowledgments)

## Overview

### The challenge

Users should be able to:

- View the optimal layout for the component depending on their device's screen size
- See the social media share links when they click the share icon

### Screenshot

![](./images/image.png)

### Links

- Solution URL: (https://github.com/christencodes/Article-Preview-Component)
- Live Site URL: (https://christencodes.github.io/Article-Preview-Component)

## My process

### Built with

- Semantic HTML5 markup
- CSS custom properties
- Flexbox
- CSS Grid
- Mobile-first workflow
- And Love from the guys in the Boot.dev Discord💖

### What I learned

##

`window.addEventListener("resize", () => {...});`

Learned more DOM manipulation and how to add an event listener to the window object. I used this method to remove/adjust the share button behavior and links based on screen size. Additionally, in desktop view, the `social_popup` will be hidden.

```js
window.addEventListener("resize", () => {
  if (window.innerWidth > 375) {
    footer.classList.add("hidden");
    card_bottom_avatar.classList.remove("hidden");
    social_popup.classList.add("hidden");
  } else if (window.innerWidth <= 375) {
    footer.classList.remove("hidden");
    card_bottom_avatar.classList.add("hidden");
  }
});
```

##

`window.onload = () => {...};`

More exploration into the window object. I used `window.onload` to adjust the footer, share options, and which footer is shown based on the current screen size.

```js
window.onload = () => {
  if (window.innerWidth > 375) {
    footer.classList.add("hidden");
    card_bottom_avatar.classList.remove("hidden");
  } else if (window.innerWidth <= 375) {
    footer.classList.remove("hidden");
    card_bottom_avatar.classList.add("hidden");
  }
};
```

##

`element.getBoundingClientRect()`

For starters, this was my first time wrapping and event listener inside a foreach loop. I did this because I created different share buttons and footer sections for the mobile and desktop view. This way, based on the screen size, the footers will have different behaviors.

I used the `element.getBoundingClientRect()` function because I ran into a problem when attempting to use `position: absolute` on the `social_popup`. While the popup appeared great on a screen width of 1440px, resizing the screen altered it's position. One of the guys in the Boot.dev Discord Server suggested the `getBoundingClientRect()` function which provides an object with information about an elements position. Using this I was able to capture the position and tweak it so that the popup would always appear over the share icon when clicked. I also disabled the popup on screen resize so the positioning was always correct when the user clicks the share icon.

```js
shareIcon.forEach((element) => {
  element.addEventListener("click", (event) => {
    // code for smaller screen size
    if (window.innerWidth <= 375) {
      footer.classList.toggle("footer-share");
      unclicked_div.classList.toggle("hidden");
      clicked_div.classList.toggle("hidden");
    }

    if (window.innerWidth > 375) {
      // Code for larger screen width

      social_popup.classList.toggle("hidden");
      const shareX = event.target.getBoundingClientRect().left;
      const shareY = event.target.getBoundingClientRect().top;
      social_popup.style.top =
        `${
          shareY -
          social_popup.getBoundingClientRect().height / 2 -
          event.target.getBoundingClientRect().height * 2.5
        }` + "px";
      social_popup.style.left =
        `${shareX - social_popup.getBoundingClientRect().width / 2}` + "px";
    }
  });
});
```

### Continued development

- Work on semantic HTML More
- Become more organized when creating css and naming
- Use CSS grid more
- Don't always default to flexbox
- Mobile-first workflow helped me a ton! going forward I want to experiement more with doing the mobile design first.
- I want to utilize modern CSS to do more heavy lifting in the future because it has so man new features. But I'm glad I'm learning how to do these things in JS.

## Acknowledgments

Thank you Boot.dev guys for making me feel good about choosing frontend! lol
