Hey guys! In this documentation, I'll be explaining each line of `style.css` in brief, so that it is convenient for you to refer to this documentation while you code.

```
@import url('https://fonts.googleapis.com/css2?family=Cedarville+Cursive&display=swap');
```
I'm importing a cursive font for my `p` tag in `.back`, i.e, for the messages I'll write on the back of the Polaroid card from **Google Fonts**. You can get any font from there as well by simply searching your specific font or exploring their font collection. Then click on **Get embedded code**, and you can import it directly into your stylesheet.

```
* {
    margin: 0;
}
```
Removing the default browser margins.

```
body {
    background-color: #8777a6af;
    /*margin-top: 1em;*/
    display: flex;
    justify-content: center;
    align-items: center;
    -webkit-app-region: drag;

}
```
- `background-color: #8777a6af;`: setting a background color for the body.
- `margin-top: 1em;`: setting a margin from the top to make the carousel appear centered to the entire webpage. Although, in the electron app, I reduce the window size so this margin is not required as it creates a vertical scrollbar. So, I have just commented it out.
- `display: flex;`: this is also for when I make the elctron app. To be able to use `justify-content: center;` & `align-items: center;`, to center the entire carousel.
- `-webkit-app-region: drag;`: this is also for the electron app. To define what regions of the app are draggable, so I can move the widget around. This is because I remove the default frame of the app.

```
.carousel {
    margin: 1em auto;
    display: flex;
    /*gap: 1em;*/
    width: 86%;
    overflow-x: auto;
    scroll-behavior: smooth;
    anchor-name: --carousel;
    scroll-snap-type: x mandatory;
    -webkit-app-region: drag;
}
```
- `margin: 1em auto;`: to add some space between the browser window and the carousel. From top and bottom: 1em and Right and Left: auto.
- `display: flex;`: to make the Polaroid cards horizontal.
- `gap: 1em;`: to provide some gap between the Polaroid cards. Not required in the electron app as only one card is displayed at a time.
- `width: 86%;`: setting the carousel width so that it doesn't add a horizontal scrollbar to the webpage by going beyond it; thus defying the logic of a carousel.
- `overflow-x: auto;`: to add a scrollbar inside the carousel to be able to scroll the cards which later on gets removed by `display:none` as I wanted to use buttons.
- `scroll-behavior: smooth;`: making the Polaroid cards scroll appear smooth and not choppy.
- `anchor-name: --carousel;`: giving a name to the carousel using which the buttons are later positioned relative to it.
- `scroll-snap-type: x mandatory;`: to make the scroll stop at the `start` of a card and not cut the card in the middle. Later defined in the `.card-conatiner` as `scroll-snap-align:start`.
- `-webkit-app-region: drag;`: defining as draggable region in the electron app.

```
.carousel::-webkit-scrollbar {
    display: none;
}
```
Removing the scrollbar within the carousel which we set by `overflow-x: auto`.

```
.carousel::scroll-button(right),
.carousel::scroll-button(left) {
    content: ">";
    border: none;
    background-color: #F38BBD;
    box-shadow: 0px 0px 5px 3px #aeadad;
    font-size: 1rem;
    color: #EEEEEE;
    height: 30px;
    width: 30px;
    border-radius: 50%;
    cursor: pointer;
    position: fixed;
    position-anchor: --carousel;
    position-area: right;
    translate: -60%;
    -webkit-app-region: no-drag;
}
```
Creating both left and right scroll buttons. The styles are redundant so styled them together and then later changing the content and position of the left button.
- `content:">"`: setting the right button content to display '>'.
- `border: none;`: removing the default border of the button.
- `background-color: #F38BBD;`: setting a background color.
- `box-shadow: 0px 0px 5px 3px #aeadad;`: to make it appear more lifted.
- `font-size: 1rem;`: setting the size of the content.
- `color: #EEEEEE;`: setting the color of the content.
- `height: 30px;` & `width: 30px;`: setting height and width to make it a square.
- `border-radius: 50%;`: rounding the edges to make the buttons circular.
- `cursor: pointer;`: changing the cursor to pointer whenever the buttons are hovered and clicked.
- `position: fixed;`: so that they do not move around when the browser window size changes.
- `position-anchor: --carousel;`: defining relative to which element these buttons should be positioned. In our case, the carousel.
- `position-area: right;`: setting the area for both the buttons as right.
- `translate: -60%;`: to make it appear slightly over the card so it looks more like a widget app's buttons.
- `-webkit-app-region: no-drag;`: setting buttons as non-draggable area for them to be able to work. [Read Electron Documentation for further Information.](https://www.electronjs.org/docs/latest/tutorial/custom-window-interactions)

```
.carousel::scroll-button(left) {
    content: "<";
    position-area: left;
    translate: 60%;
}
```
- `content: "<";`: changing the content of the left button to make it indicate the left.
- `position-area: left;`: positioning the left button to the left of the carousel.
- `translate: 60%;`: making it appear slightly over the card.

```
.carousel::scroll-button(right):disabled,
.carousel::scroll-button(left):disabled {
    opacity: 0.5;
    cursor: auto;
}
```
Styling the buttons to disable when there are no more cards to scroll. Making their opacity lighter and cursor as auto (means the normal cursor) so that user can understand there are no more cards left to scroll.

```
.card-container {
    scroll-snap-align: start;
    flex: 0 0 15em;
    height: 20em;
    background-color: #8777a6af;
    padding: 1em;
    text-align: center;
    perspective: 1000px;
}
```
- `scroll-snap-align: start;`: Makes the carousel snap stop at the start of a card.
- `flex: 0 0 15em;`: setting the base size of the card-container as 15em. Prevents grow  and shrink properties so that the container doesn't shrink or grow outside the carousel.
- `height: 20em;`: setting height as 20em.
- `background-color: #8777a6af;`: setting background color of the card-container.
- `padding: 1em;`: providing some padding so that the card is seperated from the card-container.
- `text-align: center;`: align the text paragraph on the backside to center.
- `perspective: 1000px;`: determines the distance between the z=0 plane and the user in order to give a 3D-positioned element some perspective.

```
.card {
    width: 100%;
    height: 100%;
    transform-style: preserve-3d;
    transition: transform 0.6s;
    box-shadow: 0px 0px 10px 4px #838181;
    -webkit-app-region: no-drag;
}
```
- `width: 100%;` & `height: 100%;`: applying width and height to the card to occupy 100% of the card-container leaving the padding.
- `transform-style: preserve-3d;`: children of this element, i.e, `.front` & `.back` will be rendered in 3D space, making the flip animation look more real.
- `transition: transform 0.6s;`: applying some delay so that the flipping animation is smooth and more realizable.
- `box-shadow: 0px 0px 10px 4px #838181;`: for a more lifted effect.
- `-webkit-app-region: no-drag;`: specifying card as a non-draggable region for the flip animation to work in Electron. [Read Electron Documentation for further Information.](https://www.electronjs.org/docs/latest/tutorial/custom-window-interactions)

```
.front,
.back {
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: rgba(255, 255, 255, 0.605);
}
```
- `position: absolute;`: so that both `.front` and `.back` are stacked upon each other.
- `width: 100%;` & `height: 100%;`: they cover the `.card` entirely so that the card appears more like a real card with two faces.
- `backface-visibility: hidden;`: so that we cannot see the other face of the card, i.e, front face through the back and vice versa, mimicking a real card.
- `display: flex;`, `justify-content: center;`, `align-items: center;`: To center align all the content.
- `background-color: rgba(255, 255, 255, 0.605);`: applying background color to both front and backside of the card.

```
.front img {
    width: 12em;
    height: 13em;
    object-fit: cover;
}
```
- `width: 12em;` & `height: 13em;`: setting width and height of the image so it can be contained within the card.
- `object-fit: cover;`: so that the image doesn't get distorted and it is fit (cropped appropriately) to the size specified.

```
.front {
    flex-direction: column;
    color: #F38BBD;
}
```
- `flex-direction: column;`: to make the layout column so that the `h3` content appears below the image.
- `color: #F38BBD;`: to change the color of the text of `h3`.

```
.back {
    transform: rotateY(180deg);
    font-family: "Cedarville Cursive", cursive;
    font-weight: 500;
    font-size: 15px;

}
```
- `transform: rotateY(180deg);`: so that inittailly the backside of the back is facing towards the user, and is hidden due to `backface-visibility: hidden`.
- `font-family: "Cedarville Cursive", cursive;`: applying the imported font from google fonts.
- `font-weight: 500;`: making the font-weight thicker.
- `font-size: 15px;`: increasing the font size.

```
.card-container:hover .card {
    transform: rotateY(180deg);
}
```
Making the card flip (rotate vertically along the Y axis) by 180 degrees.

That's it for your stylesheet guys!✨

Need help with Electron: [Electron Tutorial](03_Desktop_Widget_using_Electron.md)\
Wanna clarify your concepts: [Watch my YouTube Video]()
