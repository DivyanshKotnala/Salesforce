# Salesforce

#Use Static resource 

#Upload the Static Resource
Go to Setup in Salesforce.
Search for Static Resources in the Quick Find box.
Click Static Resources.
Click New.
Fill in the required fields:
Name: Give your static resource a name (e.g., MyImageResource).
Cache Control: Choose Public or Private based on your requirements.
Upload File: Choose the file to upload (e.g., myImage.png).
Click Save.

# JS
import { LightningElement } from 'lwc';
import myImageResource from '@salesforce/resourceUrl/MyImageResource';

export default class MyComponent extends LightningElement {
    imageUrl = myImageResource;
}


#HTML
<template>
    <img src={imageUrl} alt="My Image" />
</template>
