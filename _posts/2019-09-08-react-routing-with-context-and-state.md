---
title: Make routing and declaring state in react 16.8 era
layout: post
---

With react 16.8 we have awesome things like ***useState()***  and ***Context Api***.

***useState :***

With useState we get rid of  [this type of declaring state.](https://reactjs.org/docs/state-and-lifecycle.html).  And react team made a good convention for this. When you declaring a new state you need to declare this state's setter function with same name like this:
```javascript
	const [externalImage,  setExternalImage] = useState("");
```

You can use this state like this:
```javascript
	externalImage !== ""  ?   <img src={externalImage} /> : <p>No image</p>  
```

and you can change state like this:
```javascript
	setExternalImage("https://bit.ly/2kAilrE")
```

 ***Context Api:***
 
 With context api if we don't making very complex or big things we don't need redux, mobx, storeon or something like those. We can solve our global store need like this:
 First we need to create a context and you can declare it inside of your component or you can import like module.
 ```javascript
 import {createContext} from "react";
 
 const externalImageContext = createContext(null);
 ```
 
 You need to wrap your component which you will use this context with this context
 ```javascript
	 const images = {
			externalImage, 
			setExternalImage
	 };
	 
	 
	 <externalImageContext.Provider images={images} >
		 <div id="image_wrapper">
			 <ShowImages />
		 </div>
	</externalImageContext.Provider>
 ```
 
 Yes, that's simple. Now you can use the context from your   ```<ShowImages />```  component.
 
 ***Now it's time to telling a real story***
 
 For my last client we used ruby on rails for back-end and static pages; and we used react for dynamic web application. I architectured like a monolith application. And they wanted from me a dynamic form for taking  their orders. For only this I didn't want to use react-router or something like that. I made with only using react's new features and a little bit javascript hacks.
 
 For this first I created a context:
```javascript
import { createContext } from "react";

export const FormContext = createContext(null);
```

After that I wrapped up our form components with this context and I added values we need in this context to our formContext. Then we control our previous, next buttons and changing components with this context too...

I declared a 'step' state for controlling changing components. First I gave 1 to this state for rendering first question. After that if user select an option in this question or they answered question and click the next or previous button next or previous question will be rendered with switch case.

I found that it's useful because of this I wanted to share. I hope you like it!

```javascript
import React, { useState, useRef, createContext } from 'react';
import Submit from "../Components/Submit";
import ServiceType from '../Components/ServiceType';
import Service from '../Components/Service';

import {FormContext} from "../Contexts/FormContext";
import Budget from '../Components/Budget';
import Email from '../Components/Email';
import Deadline from '../Components/Deadline';

function RequestForm(props) {
	  //===========================
		//Form Values start
		/*
		  * These are the values when we need to submit this form
		*/
		
		const [serviceType, setServiceType] = useState("service");
		const [service, setService] = useState();
		const [budgetMax, setBudgetMax] = useState(0);
		const [budgetMin, setBudgetMin] = useState(0);
		const [email, setEmail] = useState("");
		const [deadline, setDeadline] = useState(null);
		
		//Form Values end
		//===========================
		
    
		//===========================
		//Form step control start
		/*
		  * This is for controlling which component will render.
		*/
		const [step, setStep] = useState(1);
		
		//Form step control end
		//===========================

    
		//===========================
		//Next and Previous buttons start
		/*
		  * We don't show every form control buttons in every component
		  * because of that we need a value to control this.
		*/
		
		const [showNextButton, setShowNextButton] = useState(false)
		const [showPreviousButton, setShowPreviousButton] = useState(false)
		
		//Next and Previous buttons end
		//===========================
		
		
    //===========================
		//Form submitted start
		/*
		  * We need to check form is submitted
		  * for rendering error message or success message 
		*/
		
		const [formSubmitted, setFormSubmitted] = useState(false);
		
		//Form submitted end
		//===========================
		
		//===========================
		//Form errors start
		/*
		  * We store errors globally and we store them in an object.
		*/
		
		const [error, setError] = useState(null);
		
		//Form errors end
		//===========================

    const value = {
        serviceType,
        setServiceType,
        service,
        setService,
        budgetMax,
        setBudgetMax,
        budgetMin,
        setBudgetMin,
        email,
        setEmail,
        step,
        setStep,
        deadline,
        setDeadline,
        formSubmitted,
        setFormSubmitted,
        showNextButton,
        setShowNextButton,
        showPreviousButton,
        setShowPreviousButton
    };

    return(
        <React.Fragment>
            {
                formSubmitted ==! true ?
                
                    <FormContext.Provider value={value}>
                    {
                        (
                            () => {
                                switch (step) {
                                    case 1:
                                            return <ServiceType />
                                        break;
                                    case 2:
                                            return <Service />
                                        break;
                                    case 3:
                                            return <Budget />
                                        break;
                                    case 4:
                                        return <Deadline />    
                                        break;

                                    case 5:
                                        return <Email />
                                    default:
                                        break;
                                }
                            }
                        )()
                    }
                    <Submit />
                </FormContext.Provider>
                
                :   <div id="form_submitted_text">
                        <p>Thank you for filling this form.</p>
                        <p> We'll touch with you soon</p>
                    </div>
            }
        </React.Fragment>
    )
}

export default RequestForm; 
```