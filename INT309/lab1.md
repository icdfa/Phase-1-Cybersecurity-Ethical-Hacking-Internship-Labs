

## **INT309: Web Technologies and Database Security – Lab 1: Introduction to Web Technologies and Understanding HTTP and HTTPS**

### **Overview**
In this lab, you will delve into the foundational concepts of web technologies, specifically focusing on the HTTP and HTTPS protocols that enable seamless communication between clients (browsers) and servers. You will learn about the structure of web requests and responses, the significance of various HTTP methods, and the critical importance of securing web traffic through HTTPS. This knowledge will lay the groundwork for understanding more complex topics in web and database security.

### **Prerequisites**
- Basic familiarity with web application concepts (HTML, CSS, JavaScript).
- Access to a modern web browser (e.g., Chrome, Firefox) and a text editor (e.g., VSCode, Notepad++).
- Understanding of client-server architecture and the basics of networking.

### **Lab Objectives**
- Grasp the fundamental components of web technologies and their roles.
- Analyze the structure and functionality of HTTP and HTTPS.
- Understand the implications of HTTP status codes and headers.
- Learn how to inspect and analyze web traffic using browser tools.

### **Exercise Instructions**

#### **Exercise 1: Creating a Simple Web Page**

1. **Create a New HTML File**:
   - Open your text editor and create a new file named `index.html`.

2. **Write HTML Code**:
   - Construct a basic web page that includes:
     - A title reflecting the content of the page.
     - A header that introduces the topic.
     - A paragraph explaining the importance of web technologies.
     - An image that visually represents web technologies (you can use a placeholder image).
     - A link to an external resource for further learning.
   - **Example Code**:
     ```html
     <!DOCTYPE html>
     <html lang="en">
     <head>
         <meta charset="UTF-8">
         <meta name="viewport" content="width=device-width, initial-scale=1.0">
         <title>Introduction to Web Technologies</title>
         <style>
             body { font-family: Arial, sans-serif; margin: 20px; }
             header { background-color: #f2f2f2; padding: 10px; }
             img { max-width: 100%; height: auto; }
         </style>
     </head>
     <body>
         <header>
             <h1>Understanding Web Technologies</h1>
         </header>
         <p>Web technologies are essential for creating and maintaining dynamic websites that facilitate user interaction.</p>
         <img src="https://via.placeholder.com/600x300" alt="Web Technologies">
         <p>Learn more about web technologies <a href="https://www.w3schools.com">here</a>.</p>
     </body>
     </html>
     ```

3. **Open in Browser**:
   - Save the `index.html` file and open it in your web browser to view the web page you created.

4. **Reflection**:
   - Discuss what you learned about the structure of HTML documents. How do elements such as headers, paragraphs, and links contribute to a web page’s content and usability?

---

#### **Exercise 2: Analyzing HTTP Requests and Responses**

1. **Use Developer Tools**:
   - Open your browser’s developer tools (F12 or right-click → Inspect) and navigate to the **Network** tab.

2. **Refresh the Web Page**:
   - With the Network tab open, refresh your page to monitor the network requests being made.

3. **Inspect HTTP Requests**:
- Click on the first request for

```bash
index.html
```

     - **Request URL**: The address of the resource.
     - **Request Method**: Understand different methods (GET, POST, etc.).
     - **Response Status Code**: What does a status code of `200 OK` mean?
     - **Response Headers**: Review headers like `Content-Type`, `Cache-Control`, and `Date`.

4. **Reflection**:
   - Analyze the significance of each element. Why is it important to understand these components when developing or securing web applications? Discuss the potential vulnerabilities associated with improperly handled requests and responses.

---

#### **Exercise 3: Understanding HTTPS and Its Importance**

1. **Access a Secure Website**:
   - In your web browser, navigate to a website that uses HTTPS (e.g., https://www.google.com).

2. **Inspect HTTPS Traffic**:
   - Open the developer tools and examine the network requests. Note how HTTPS requests are displayed differently compared to HTTP requests.

3. **Explore the Security Information**:
   - Click on the padlock icon in the address bar. Investigate the security certificate details, including:
     - Certificate issuer
     - Validity period
     - Encryption methods used

4. **Reflection**:
   - Discuss the advantages of using HTTPS over HTTP, particularly in terms of data security and privacy. What protections does HTTPS provide against attacks such as eavesdropping and man-in-the-middle (MitM)?

---

### **Report Submission**
At the end of this lab, you are required to submit a comprehensive report summarizing your findings and reflections from each exercise. Your report should include:

- An overview of web technologies, including a summary of their importance.
- Detailed reflections from each exercise, emphasizing key observations about HTTP and HTTPS.
- Screenshots of your web page, network requests, and security certificate details.
- Any additional insights or recommendations regarding web technologies and secure communications.

**Submission Format**: Submit your report as a PDF file. Ensure that it is well-organized, clear, and addresses each aspect of the lab.

---

### **Conclusion**
In this lab, you explored the foundational concepts of web technologies, including the workings of HTTP and HTTPS protocols. Understanding these concepts is vital for developing and securing web applications effectively.

