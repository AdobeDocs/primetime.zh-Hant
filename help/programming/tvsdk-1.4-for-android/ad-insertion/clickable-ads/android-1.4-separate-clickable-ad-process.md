---
description: 您應將播放器的UI邏輯與管理廣告點按的程式區隔。 其中一個方法是為活動實作多個片段。
seo-description: 您應將播放器的UI邏輯與管理廣告點按的程式區隔。 其中一個方法是為活動實作多個片段。
seo-title: 區隔可點按的廣告流程
title: 區隔可點按的廣告流程
uuid: 00537191-8997-418d-add2-8e86d818c76e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 區隔可點按的廣告流程{#separate-the-clickable-ad-process}

您應將播放器的UI邏輯與管理廣告點按的程式區隔。 其中一個方法是為活動實作多個片段。

1. 實作一個片段以包 `MediaPlayer` 含，並負責視訊播放。

   此片段應呼叫 `notifyClick`。

   ```java
   public class PlayerFragment extends SherlockFragment { 
       ... 
       public void notifyAdClick () { 
           _mediaPlayer.notifyClick(); 
       } 
       ... 
   } 
   ```

1. 實作不同的片段，以顯示指出廣告可點按的UI元素、監控該UI元素，以及將使用者點按次數傳達給包含該片段的片段 `MediaPlayer`。

   此片段應聲明用於片段通信的介面。 該片段在其onAttach生命週期方法期間捕獲介面實現，並可調用介面方法以與活動通信。

   ```java
   public class PlayerClickableAdFragment extends SherlockFragment { 
       private ViewGroup viewGroup; 
       private Button button; 
       OnAdUserInteraction callback; 
   
       @Override 
       public View onCreateView(LayoutInflater inflater,  
                                ViewGroup container, Bundle 
                                savedInstanceState) { 
   
           // the custom fragment is defined by a custom button 
           viewGroup =  
             (ViewGroup) inflater.inflate(R.layout.fragment_player_clickable_ad, container, false); 
           button = (Button) viewGroup.findViewById(R.id.clickButton); 
   
           // register a click listener to detect user interaction 
           button.setOnClickListener(new View.OnClickListener() { 
               @Override 
               public void onClick(View v) { 
                   // send the event back to the activity 
                   callback.onAdClick(); 
               } 
           }); 
   
           viewGroup.setVisibility(View.INVISIBLE); 
           return viewGroup; 
       } 
   
       public void hide() { 
           viewGroup.setVisibility(View.INVISIBLE); 
       } 
   
       public void show() { 
           viewGroup.setVisibility(View.VISIBLE);  
       } 
   
       @Override 
       public void onAttach(Activity activity) { 
           super.onAttach(activity); 
           // attaches the interface implementation 
           // if the container activity does not implement the methods  
           // from the interface an exception will be thrown 
           try { 
               callback = (OnAdUserInteraction) activity; 
           } catch (ClassCastException e) { 
               throw new ClassCastException(activity.toString() 
               + " must implement OnAdUserInteraction"); 
           }  
       } 
   
       // user defined interface that allows fragment communication 
       // must be implemented by the container activity 
       public interface OnAdUserInteraction { 
           public void onAdClick(); 
       } 
   } 
   ```

