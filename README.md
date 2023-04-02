## Create a Drag and Drop file component in ReactJS, NextJS & Tailwind

![](https://miro.medium.com/v2/resize:fit:1400/1*8TF4QOC7y71DOxdkeBN65A.gif)

In this tutorial, I’ll walk you through how to build a drag and drop zone component. This component will also allow users to select files with the file explorer, update the files selected, remove files selected and display the list of files selected.

We use one of React’s many frameworks, NextJS as well as tailwind css to style our components.

Learn more about these technologies here

[Start a New React Project — React](https://react.dev/learn/start-a-new-react-project)

[Install Tailwind CSS with Next.js — Tailwind CSS](https://tailwindcss.com/docs/guides/nextjs)

**Let’s Begin**

Inside our NextJs src/app/ directory we create a new directory called  **dragAndDrop (or anything really)** as well as a page.tsx file inside of it as our main route.

![](https://miro.medium.com/v2/resize:fit:1400/1*tWNcr1D6KgGhU-5t3EMDpA.png)

Let’s do the initial setups and imports for our component. We add the  **‘use client’** statement to specify to Next JS that this is a client component. This will allow us to use client-side features like event listeners etc. We also import  **useRef** and  **useState** from react.

    "use client";  
      
    import { useRef, useState } from "react";  
      
    export default function DragAndDrop() {  
      
      return (  
       <div></div>  
      );  
    }

Next, we initialize some states and reference. We will use  **dragActive** state to track when a file has entered or exited the dropzone. The  **inputRef** will be used to activate the choose file dialogue box, and the  **files** state will be used to store our files.

    "use client";  
      
    import { useRef, useState } from "react";  
      
    export default function DragAndDrop() {  
      
      const [dragActive, setDragActive] = useState<boolean>(false);  
      const inputRef = useRef<any>(null);  
      const [files, setFiles] = useState<any>([]);  
      
      return (  
       <div></div>  
      );  
    }

Next, we add a form component and center it inside a parent div element. We give it some styling using tailwind and also add some event listener properties. We include a conditional color change using the  **dragActive** state that will change to a darker blue color when a user drags a file into the drop zone.

    "use client";  
      
    import { useRef, useState } from "react";  
    export default function DragAndDrop() {  
      
      return (  
        <div className="flex items-center justify-center h-screen">  
          <form  
            className={`${  
              dragActive ? "bg-blue-400" : "bg-blue-100"  
            }  p-4 w-1/3 rounded-lg  min-h-[10rem] text-center flex flex-col items-center justify-center`}  
            onDragEnter={handleDragEnter}  
            onSubmit={(e) => e.preventDefault()}  
            onDrop={handleDrop}  
            onDragLeave={handleDragLeave}  
            onDragOver={handleDragOver}  
          >  
       
          </form>  
        </div>  
      );  
    }

Let’s add an input element and some text that will be responsible for opening up the select file explorer when activated. We will set this input element to hidden and attach its ref to be activated when the  **Select Files** text is selected.

![](https://miro.medium.com/v2/resize:fit:1400/1*g9pcWW0PK3rcbwZsxmazXA.png)

    "use client";  
      
    import { useRef, useState } from "react";  
    export default function DragAndDrop() {  
      
      return (  
        <div className="flex items-center justify-center h-screen">  
          <form  
            className={`${  
              dragActive ? "bg-blue-400" : "bg-blue-100"  
            }  p-4 w-1/3 rounded-lg  min-h-[10rem] text-center flex flex-col items-center justify-center`}  
            onDragEnter={handleDragEnter}  
            onSubmit={(e) => e.preventDefault()}  
            onDrop={handleDrop}  
            onDragLeave={handleDragLeave}  
            onDragOver={handleDragOver}  
          >  
      
           <input  
              placeholder="fileInput"  
              className="hidden"  
              ref={inputRef}  
              type="file"  
              multiple={true}  
              onChange={handleChange}  
              accept=".xlsx,.xls,image/*,.doc, .docx,.ppt, .pptx,.txt,.pdf"  
            />  
      
            <p>  
              Drag & Drop files or{" "}  
              <span  
                className="font-bold text-blue-600 cursor-pointer"  
                onClick={openFileExplorer}  
              >  
                <u>Select files</u>  
              </span>{" "}  
              to upload  
            </p>  
       
          </form>  
        </div>  
      );  
    }

We will finally add a component to display all the current selected or dropped files with a remove option beside them. We use the map function to map through our file state and display the name of each file along with a text that will remove the file from the selected list. We pass the file name as well as the index of the file to the remove file function.

![](https://miro.medium.com/v2/resize:fit:1400/1*KHUftAO29DwjAdOn3KNGpw.png)

    "use client";  
      
    import { useRef, useState } from "react";  
    export default function DragAndDrop() {  
      
      return (  
        <div className="flex items-center justify-center h-screen">  
          <form  
            className={`${  
              dragActive ? "bg-blue-400" : "bg-blue-100"  
            }  p-4 w-1/3 rounded-lg  min-h-[10rem] text-center flex flex-col items-center justify-center`}  
            onDragEnter={handleDragEnter}  
            onSubmit={(e) => e.preventDefault()}  
            onDrop={handleDrop}  
            onDragLeave={handleDragLeave}  
            onDragOver={handleDragOver}  
          >  
      
           <input  
              placeholder="fileInput"  
              className="hidden"  
              ref={inputRef}  
              type="file"  
              multiple={true}  
              onChange={handleChange}  
              accept=".xlsx,.xls,image/*,.doc, .docx,.ppt, .pptx,.txt,.pdf"  
            />  
      
            <p>  
              Drag & Drop files or{" "}  
              <span  
                className="font-bold text-blue-600 cursor-pointer"  
                onClick={openFileExplorer}  
              >  
                <u>Select files</u>  
              </span>{" "}  
              to upload  
            </p>  
      
          <div className="flex flex-col items-center p-3">  
              {files.map((file: any, idx: any) => (  
                <div key={idx} className="flex flex-row space-x-5">  
                  <span>{file.name}</span>  
                  <span  
                    className="text-red-500 cursor-pointer"  
                    onClick={() => removeFile(file.name, idx)}  
                  >  
                    remove  
                  </span>  
                </div>  
              ))}  
            </div>  
       
          </form>  
        </div>  
      );  
    }

Now that the interface is done, let’s write our functions. This will include;

-   **handleDragEnter —** This will track when a file has entered the drop zone. We will use this to change our zone color to let the user know that the zone is currently active. We set the  **dragActive** to true which will trigger the css color change in our form component.
-   **handleDrop —** This will track when a file has been dropped into the zone. We get the event passed from the form, iterate through the file list and store each file in our files state.
-   **handleDragLeave —** This will track when a file leaves our zone. We will use this to set  **dragActive** to false in order to set our zone color back to default.
-   **handleDragOver —** This will track when a file is dragged over our zone. We set the  **dragActive** to true which will trigger the zone color change.
-   **openFileExplorer —** Remember we wanted our input element hidden? When we did this, we also attached a ref to our  **Select Files** text which will open up the input files dialog when clicked. This function will help activate the hidden input element to bring up the file explorer box.
-   **removeFile —** This function will remove a selected file from the list.
-   **handleChange —** This function will track when a file has been added through our file explorer dialog. This will iterate through the file list and store each file in our files state.
-   **handleSubmit —** Use this function to write your own submit logic. It first checks if our file list contains any files.

  

      "use client";  
          
        import { useRef, useState } from "react";  
        export default function DragAndDrop() {  
          
          function handleChange(e: any) {  
            e.preventDefault();  
            console.log("File has been added");  
            if (e.target.files && e.target.files[0]) {  
              for (let i = 0; i < e.target.files["length"]; i++) {  
                setFiles((prevState: any) => [...prevState, e.target.files[i]]);  
              }  
            }  
          }  
          
          function handleSubmitFile(e: any) {  
            if (files.length === 0) {  
              // no file has been submitted  
            } else {  
              // write submit logic here  
            }  
          }  
          
          function handleDrop(e: any) {  
            e.preventDefault();  
            e.stopPropagation();  
            setDragActive(false);  
            if (e.dataTransfer.files && e.dataTransfer.files[0]) {  
              for (let i = 0; i < e.dataTransfer.files["length"]; i++) {  
                setFiles((prevState: any) => [...prevState, e.dataTransfer.files[i]]);  
              }  
            }  
          }  
          
          function handleDragLeave(e: any) {  
            e.preventDefault();  
            e.stopPropagation();  
            setDragActive(false);  
          }  
          
          function handleDragOver(e: any) {  
            e.preventDefault();  
            e.stopPropagation();  
            setDragActive(true);  
          }  
          
          function handleDragEnter(e: any) {  
            e.preventDefault();  
            e.stopPropagation();  
            setDragActive(true);  
          }  
          
          function removeFile(fileName: any, idx: any) {  
            const newArr = [...files];  
            newArr.splice(idx, 1);  
            setFiles([]);  
            setFiles(newArr);  
          }  
          
          function openFileExplorer() {  
            inputRef.current.value = "";  
            inputRef.current.click();  
          }  
          
          return (  
            <div className="flex items-center justify-center h-screen">  
              <form  
                className={`${  
                  dragActive ? "bg-blue-400" : "bg-blue-100"  
                }  p-4 w-1/3 rounded-lg  min-h-[10rem] text-center flex flex-col items-center justify-center`}  
                onDragEnter={handleDragEnter}  
                onSubmit={(e) => e.preventDefault()}  
                onDrop={handleDrop}  
                onDragLeave={handleDragLeave}  
                onDragOver={handleDragOver}  
              >  
          
               <input  
                  placeholder="fileInput"  
                  className="hidden"  
                  ref={inputRef}  
                  type="file"  
                  multiple={true}  
                  onChange={handleChange}  
                  accept=".xlsx,.xls,image/*,.doc, .docx,.ppt, .pptx,.txt,.pdf"  
                />  
          
                <p>  
                  Drag & Drop files or{" "}  
                  <span  
                    className="font-bold text-blue-600 cursor-pointer"  
                    onClick={openFileExplorer}  
                  >  
                    <u>Select files</u>  
                  </span>{" "}  
                  to upload  
                </p>  
          
              <div className="flex flex-col items-center p-3">  
                  {files.map((file: any, idx: any) => (  
                    <div key={idx} className="flex flex-row space-x-5">  
                      <span>{file.name}</span>  
                      <span  
                        className="text-red-500 cursor-pointer"  
                        onClick={() => removeFile(file.name, idx)}  
                      >  
                        remove  
                      </span>  
                    </div>  
                  ))}  
                </div>  
           
              </form>  
            </div>  
          );  
        }

**Full Code here**

    "use client";  
      
    import { useRef, useState } from "react";  
    export default function DragAndDrop() {  
      const [dragActive, setDragActive] = useState<boolean>(false);  
      const inputRef = useRef<any>(null);  
      const [files, setFiles] = useState<any>([]);  
      
      function handleChange(e: any) {  
        e.preventDefault();  
        console.log("File has been added");  
        if (e.target.files && e.target.files[0]) {  
          console.log(e.target.files);  
          for (let i = 0; i < e.target.files["length"]; i++) {  
            setFiles((prevState: any) => [...prevState, e.target.files[i]]);  
          }  
        }  
      }  
      
      function handleSubmitFile(e: any) {  
        if (files.length === 0) {  
          // no file has been submitted  
        } else {  
          // write submit logic here  
        }  
      }  
      
      function handleDrop(e: any) {  
        e.preventDefault();  
        e.stopPropagation();  
        setDragActive(false);  
        if (e.dataTransfer.files && e.dataTransfer.files[0]) {  
          for (let i = 0; i < e.dataTransfer.files["length"]; i++) {  
            setFiles((prevState: any) => [...prevState, e.dataTransfer.files[i]]);  
          }  
        }  
      }  
      
      function handleDragLeave(e: any) {  
        e.preventDefault();  
        e.stopPropagation();  
        setDragActive(false);  
      }  
      
      function handleDragOver(e: any) {  
        e.preventDefault();  
        e.stopPropagation();  
        setDragActive(true);  
      }  
      
      function handleDragEnter(e: any) {  
        e.preventDefault();  
        e.stopPropagation();  
        setDragActive(true);  
      }  
      
      function removeFile(fileName: any, idx: any) {  
        const newArr = [...files];  
        newArr.splice(idx, 1);  
        setFiles([]);  
        setFiles(newArr);  
      }  
      
      function openFileExplorer() {  
        inputRef.current.value = "";  
        inputRef.current.click();  
      }  
      
      return (  
        <div className="flex items-center justify-center h-screen">  
          <form  
            className={`${  
              dragActive ? "bg-blue-400" : "bg-blue-100"  
            }  p-4 w-1/3 rounded-lg  min-h-[10rem] text-center flex flex-col items-center justify-center`}  
            onDragEnter={handleDragEnter}  
            onSubmit={(e) => e.preventDefault()}  
            onDrop={handleDrop}  
            onDragLeave={handleDragLeave}  
            onDragOver={handleDragOver}  
          >  
            {/* this input element allows us to select files for upload. We make it hidden so we can activate it when the user clicks select files */}  
            <input  
              placeholder="fileInput"  
              className="hidden"  
              ref={inputRef}  
              type="file"  
              multiple={true}  
              onChange={handleChange}  
              accept=".xlsx,.xls,image/*,.doc, .docx,.ppt, .pptx,.txt,.pdf"  
            />  
      
            <p>  
              Drag & Drop files or{" "}  
              <span  
                className="font-bold text-blue-600 cursor-pointer"  
                onClick={openFileExplorer}  
              >  
                <u>Select files</u>  
              </span>{" "}  
              to upload  
            </p>  
      
            <div className="flex flex-col items-center p-3">  
              {files.map((file: any, idx: any) => (  
                <div key={idx} className="flex flex-row space-x-5">  
                  <span>{file.name}</span>  
                  <span  
                    className="text-red-500 cursor-pointer"  
                    onClick={() => removeFile(file.name, idx)}  
                  >  
                    remove  
                  </span>  
                </div>  
              ))}  
            </div>  
      
            {/* <button  
              className="bg-black rounded-lg p-2 mt-3 w-auto"  
              onClick={handleSubmitFile}  
            >  
              <span className="p-2 text-white">Submit</span>  
            </button> */}  
          </form>  
        </div>  
      );  
    }

![](https://miro.medium.com/v2/resize:fit:1400/1*8TF4QOC7y71DOxdkeBN65A.gif)

