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
Angular에서 관리하는 이벤트의 경우에는 two way binding을 통해서 화면 업데이트가 가능하다. cordova plugin이나 서버통신과 같이 외부로부터 비동기적으로 받는 이벤트의 발생 후에 화면 변경을 해야하는 경우 NgZone을 사용한다.
NgZone은 Angular 모듈이 change Detection을 수행하도록 한다.
```
this.ngZone.run(()=>{
  this.changeThisPlz = JSON.stringify(msg);
});
```

## 이벤트
```

import { Events } from 'ionic-angular';

// first page (publish an event when a user is created)
constructor(public events: Events) {}
createUser(user) {
  console.log('User created!')
  this.events.publish('user:created', user, Date.now());
}


// second page (listen for the user created event after function is called)
constructor(public events: Events) {
  events.subscribe('user:created', (user, time) => {
    // user and time are the same arguments passed in `events.publish(user, time)`
    console.log('Welcome', user, 'at', time);
  });
}

```
