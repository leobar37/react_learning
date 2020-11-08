
# overview

lets face it, forms  are really verbose 
in `React` , to make matter worse, 
most form helper do wayy too much magic and often 
have and often have a significant performnce cost
associated with them
.
Formik is a small libray that helps you with 
the  most annonyng parts .

-  getting values in and out of forms state 
-  Validations and error messages 
- Handling form submission 

Formik keeps trach of your form's state 
and the sxposes it plus a few reusable methods
and event handlers 


```js
 const  sendForm = (values ,{ setSubmitting  })=>{
            
      setTimeout(()=>{
          alert(JSON.stringify(values, null , 3));
      }, 1000);
   }

    return (
        <div> 
             <Formik initialValues={user}  validate= {validateForm} onSubmit= { sendForm}>
                  { 
                     ({ errors , touched  })=>{
                       return   <Form className="container">
                              <Field className="form-control" placeholder="email" type="email" name="email" />
                              <ErrorMessage name="email" component="div" /> 
                        
                              <Field className="form-control" placeholder="password" type="password" name="password"/>
                              <ErrorMessage  name="password" component="div"/>
                              <Button type="submit" variant="success"  >submit</Button>
                          </Form>
                     }
                    }
             </Formik>
        </div>
    )
}
```

## a simpre newsletter signup form

```js
import React from 'react';
 import { useFormik } from 'formik';
 
 const SignupForm = () => {
   // Pass the useFormik() hook initial form values and a submit function that will
   // be called when the form is submitted
   const formik = useFormik({
     initialValues: {
       email: '',
     },
     onSubmit: values => {
       alert(JSON.stringify(values, null, 2));
     },
   });
   return (
     <form onSubmit={formik.handleSubmit}>
       <label htmlFor="email">Email Address</label>
       <input
         id="email"
         name="email"
         type="email"
         onChange={formik.handleChange}
         value={formik.values.email}
       />
       <button type="submit">Submit</button>
     </form>
   );
 };
```
we pass our forms `initialValues` and submission function `submit` 
to the `useFormik` hook, the hook then result as googdie bag of
form state and helpers in variable we are calling `formik`

**in the goodie bag the are buch of helpers methods, but for now the one we care about as follow**
- *handleSubmit:* A submission handler
- *handleChange:* A change handler to pas to each  `input`  `select` `textArea`
- *values*  : Our form's current values



