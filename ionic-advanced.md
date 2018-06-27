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
