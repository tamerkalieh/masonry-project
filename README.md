# Vite - Masonry

I have a few things to tell before you going through the application. This project is a simple app and not an application that has any commercial use.

I had requirements such as using the pinia store.

However, I decided not to use pinia since this simple app does not require such a too.. Pinia is meant to be a store that makes information cross-component accessible. A good usecase is showing user-informaiton such as the name in the navigation as well as printing out user-data in some profile page.

However, for this simple application I had no need in pushing random generated images to the store, neither the flag information for each of the images.

---

Further, there are a few improvements that can be made but I was not able to do them in the timeframe that was given.

## 1. Card Wrapper

The "Masonry-Wrapper" could be some UiCard that displays any content you can think off. So instead of just adding the masonry layout inside the card, the card could have a slot. This slot can be then used to show the masonry layout or any other content.

## 2. UiImage Component

The image itself could be a component that includes the "flag-select" as a child component. The App.vue would then pass down each image to the UiImage component which then displays the flag-select.

## 4. SVG Flag

I could have added the flag as an `<img />` or include it with JS, but there is no need for that in a simple application like that so I just pasted a minified version of the SVG. I tried to extract the flag from figma but somehow wasn't able to get it.

