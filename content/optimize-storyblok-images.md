---
title: Optimize Background Images Sourced From Storyblok in Gatsby
description: 'Learn how to optimize background images in Storyblok Headless CMS to improve performance'
image: https://via.placeholder.com/150
---

In this tutorial, I am going to show you how to serve optimized background images sourced from Storyblok (The Only Headless CMS with a Visual Editor). I assume you are familiar with Gatsby and Storyblok. If you are not familiar with these, visit this link; The Complete Guide to Build a Full-Blown Multilanguage Website with Gatsby.js to get up to speed.

## The Challenge

The **gatsby-image** plugin is what is generally used to serve optimized images in Gatsby. The challenge, however, is the fact that gatsby-image plugin (as at the time of writing) works for images from the file system. This poses a challenge to the various Headless CMS available.

When your content comes from the Headless CMS you lose the optimization of your images if the CMS does not provide a way for you to utilize the gatsby-image plugin. The **gatsby-storyblok-image** package helps us when using Storyblok.

One faces an extra hurdle when you want to use an optimized background image. Luckily for us, we already have the **gatsby-background-image** plugin helps with background images.

## The Proposed Solution

We are going to combine the gatsby-background-image and gatsby-storyblok-image plugins to achieve this. This implementation is what I used in my blog. The blog is open-sourced and can be downloaded over here. You can get the full version from there.

```bash
yarn add gatsby-background-image gatsby-storyblok-image styled-components
```
Create helper functions in a file **src/utils/gatsbyImageTransform.js** to use the fluid and fixed queries provided by gatsby-storyblok-image

```js{1,3-5}[gatsbyImageTransform.js]

import { getFixedGatsbyImage, getFluidGatsbyImage } from "gatsby-storyblok-image"
export const fluidImage = (image, params) => {
  const fluidProps = getFluidGatsbyImage(image, { ...params })
  return fluidProps
}
export const fixedImage = (image, params) => {
  const fixedProps = getFixedGatsbyImage(image, { ...params })
  return fixedProps
}
```

Create a hero component, hero.js that uses the helper function to serve optimized background images

```js{1,3-5}[hero.js]

import React from "react"
import SbEditable from "storyblok-react"
import styled from "styled-components"
import BackgroundImage from "gatsby-background-image"

import { fluidImage } from "../../utils/gatsbyImageTransform"

const Hero = props => {
  let optimizedFluidImage = fluidImage(props.blok.banner)
  return (
    <SbEditable content={props.blok}>
      <Wrapper fluid={optimizedFluidImage}>
        <Overlay />
        <Heading>{props.blok.heading}</Heading>
        {props.path === "index" && props.blok.description && (
          <Description>{props.blok.description}</Description>
        )}
      </Wrapper>
    </SbEditable>
  )
}
export default Hero
const Wrapper = styled(props => <BackgroundImage {...props} />)`
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  height: 50vh;
  margin-bottom: 2em;
  }
`
const Heading = styled.h2`
  z-index: 2;
  color: #06c4d1;
  font-size: 5em;
  @media (max-width: 768px) {
    font-size: 2.3em;
  }
`
const Description = styled.p`
  color: #fff;
  z-index: 2;
  font: 400 25px/33px "Montserrat";
  @media (max-width: 768px) {
    font-size: 15px;
  }
`
const Overlay = styled.div`
  position: absolute;
  top: 0px;
  left: 0px;
  width: 100%;
  height: 100%;
  background-color: rgb(19, 17, 16);
  opacity: 0.7;
`
```

The helper function is what provides the image data: fluidImage and fixedImage that is supplied to the BackgroundImage component which is later used as the background image for the hero component.


## A Quick Recap

We looked at how to serve optimized background images to the visitors of our website. It involved 2 open-sourced packages; the gatsby-background-image and gatsby-storyblok-image packages. We use the former to get the image data that is used originally in the gatsby-image plugin and supply this data to the gatsby-background-image plugin to be able to achieve the optimization we need.

I'd like to hear your views about this approach and the alternatives you might have used in your project. The gatsby-storyblok-image package is also quite young so the open-source community will be very helpful in bringing all the features gatsby-image provides.

[Back](/articles)