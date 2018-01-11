use different style for different elements number

```css
div:first-child:nth-last-child(2)
```

解读： div中第一元素等同于倒数第二个元素时，说明一共只有两个元素

Example

```css
  .video:first-child:nth-last-child(1) {
    float: left;
    height: 100%;
    width: 100%;
  }

  .video:first-child:nth-last-child(2) {
    &, & ~ .video {
      float: left;
      height: 100%;
      width: 50%;
    }
  }

  .video:first-child:nth-last-child(3) {
    &, & ~ .video {
      float: left;
      height: 50%;
      width: 50%;
    }
  }

  .video:first-child:nth-last-child(4) {
    &, & ~ .video {
      float: left;
    }

    & {
      height: 100%;
      width: 70%;
    }

    & ~ :nth-child(n + 1) {
      height: 25%;
      width: 30%;
    }
  }
```



