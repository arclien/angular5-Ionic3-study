# Ionic Advanced Components

## Gesture
[참고](https://ionicframework.com/docs/components/#gestures)

Basic gestures can be accessed from HTML by binding to tap, press, pan, swipe, rotate, and pinch events.

```
<ion-card (swipe)="swipeCategory($event)">
...
</ion-card>

swipeCategory(event){
  let index = this.categories.indexOf(this.categorySelected);
  if( event.direction == 4){
    //Swipe Right is 4
    if(index >= 1){
      this.categoryChange(this.categories[index-1]);
    }
  }else if( event.direction == 2 ){
    //Swipe Left is 2
    if( index < this.categories.length-1 ){
      this.categoryChange(this.categories[index+1]);
    }
  }
}
categoryChange(category){
  // change category index
  // set current category selected
  // change menu
}
```

## Infinite Scroll
[참고](https://ionicframework.com/docs/api/components/infinite-scroll/InfiniteScroll/)

The Infinite Scroll allows you to perform an action when the user scrolls a specified distance from the bottom or top of the page.

```

<ion-content>

 <ion-list>
   <ion-item *ngFor="let i of items">{{i}}</ion-item>
 </ion-list>

 <ion-infinite-scroll (ionInfinite)="doInfinite($event)">
   <ion-infinite-scroll-content></ion-infinite-scroll-content>
 </ion-infinite-scroll>

</ion-content>
```
```
doInfinite(infiniteScroll) {
  console.log('Begin async operation');

  setTimeout(() => {
    for (let i = 0; i < 30; i++) {
      this.items.push( this.items.length );
    }

    console.log('Async operation has ended');
    infiniteScroll.complete();
  }, 500);
}
```

## NgZone

