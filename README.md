# Java Servlet and JSP Practicals

## PRACTICAL NO: 1
### **AIM**
Implement the following Simple Servlet application.

### 🅐 Simple Calculator Application using Servlet

**Algorithm:** Create a calculator that performs basic arithmetic operations (+, -, *, /) based on user input.

**index.html:**
```html
<html>
<head>
<title>Simple Calculator</title>
</head>
<body>
<form action="check" method="get">
Enter number 1:<input type="text" name="n1">
Enter number 2:<input type="text" name="n2">
Select Operator:<select name="operator">
<option value="+">+</option>
<option value="-">-</option>
<option value="*">*</option>
<option value="/">/</option>
</select>
<input type="submit" value="Calculate">
<input type="reset" value="Reset">
</form> 
</body> 
</html>
```

**check.java:**
```java
import java.io.*;
import javax.servlet.*;

public class check extends GenericServlet {
    public void service(ServletRequest req, ServletResponse res)
    throws ServletException, IOException {
        PrintWriter out = res.getWriter();
        int a = Integer.parseInt(req.getParameter("n1"));
        int b = Integer.parseInt(req.getParameter("n2"));
        String op = req.getParameter("operator");
        
        if(op.equals("+")) {
            out.println("Addition is: " + (a + b));
        }
        else if(op.equals("-")) {
            out.println("Subtraction is: " + (a - b));
        }
        else if(op.equals("*")) {
            out.println("Multiplication is: " + (a * b));
        }
        else {
            out.println("Division is: " + (a / b));
        }
    }
}
```

### 🅑 Login Page Servlet

**Algorithm:** Validate username and password, display appropriate message based on authentication result.

**index.html:**
```html
<html>
<head>
<title>Login Page</title>
</head>
<body>
<form action="Demo">
Enter UserName: <input type="text" name="n1"><br>
Enter Password: <input type="password" name="n2"><br><br>
<input type="submit" value="Login">
<input type="reset" value="Reset">
</form>
</body>
</html>
```

**Demo.java:**
```java
import java.io.*;
import javax.servlet.*;

public class Demo extends GenericServlet {
    public void service(ServletRequest req, ServletResponse res)
    throws ServletException, IOException {
        PrintWriter out = res.getWriter();
        String n1 = req.getParameter("n1");
        String n2 = req.getParameter("n2");
        
        if(n1.equals("SHUBHAM") && n2.equals("115")) {
            out.println("<h1>HELLO " + n1 + "<br>");
            out.println("You are successfully logged in...</h1>");
        }
        else {
            out.println("<h1>Login Failed</h1>");
        }
    }
}
```

### 🅒 Registration Servlet with JDBC

**Algorithm:** Accept user registration details and store them in database using JDBC.

**index.html:**
```html
<html>
<head>
<title>Registration Servlet</title>
</head>
<body>
<form action="register" method="get">
Enter Username:<input type="text" name="n1"><br>
Enter Password:<input type="text" name="n2"><br>
Enter E-mail:<input type="text" name="n3"><br>
Enter Country Name:<input type="text" name="n4"><br><br>
<input type="submit" value="Register">
<input type="reset" value="Reset">
</form>
</body>
</html>
```

**register.java:**
```java
import java.io.IOException;
import java.io.PrintWriter;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns = {"/register"})
public class register extends HttpServlet {
    
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
        PrintWriter out = response.getWriter();
        String s1 = request.getParameter("n1");
        String s2 = request.getParameter("n2");
        String s3 = request.getParameter("n3");
        String s4 = request.getParameter("n4");
        
        try {
            Class.forName("com.mysql.jdbc.Driver");
            Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/register","root","system");
            String sql = "Insert into register values(?,?,?,?)";
            PreparedStatement ps = con.prepareStatement(sql);
            ps.setString(1, s1);
            ps.setString(2, s2);
            ps.setString(3, s3);
            ps.setString(4, s4);
            ps.executeUpdate();
            out.println("Data Inserted!");
            con.close();
        }
        catch(Exception e) {
            out.println(e);
        }
    }
}
```

---

## PRACTICAL NO: 2
### **AIM**
Implement the following Servlet applications with Cookies and Session.

### 🅐 Request Dispatcher Interface

**Algorithm:** Validate password using Request Dispatcher, forward to welcome page if correct.

**index.html:**
```html
<html>
<head>
<title>Request Dispatcher</title>
</head>
<body>
<form action="Demo" method="get">
Enter Username:<input type="text" name="n1"><br>
Enter Password:<input type="password" name="n2"><br><br>
<input type="submit" value="Submit">
<input type="reset" value="Reset">
</form>
</body>
</html>
```

**Demo.java:**
```java
import java.io.*;
import javax.servlet.*;

public class Demo extends GenericServlet {
    public void service(ServletRequest req, ServletResponse res) 
    throws IOException, ServletException {
        PrintWriter out = res.getWriter();
        String n1 = req.getParameter("n1");
        String n2 = req.getParameter("n2");
        
        if(n2.equals("Servlet")) {
            req.setAttribute("user", n1);
            RequestDispatcher rd = req.getRequestDispatcher("welcome");
            rd.forward(req, res);
        }
        else {
            out.print("Password is invalid");
        }
    }
}
```

**welcome.java:**
```java
import java.io.*;
import javax.servlet.*;

public class welcome extends GenericServlet {
    public void service(ServletRequest req, ServletResponse res)
    throws IOException, ServletException {
        String s = (String)req.getAttribute("user");
        PrintWriter out = res.getWriter();
        out.print("<h1>Hello " + s + "<br>You are Welcome here.</h1>");
    }
}
```

### 🅑 Cookies for Visit Counter

**Algorithm:** Use cookies to store and track the number of visits to servlet.

**index.html:**
```html
<html>
<head>
<title>Using Cookies</title>
</head>
<body>
<form action="cookie">
<input type="submit" value="Go to servlet for visiting counter"/>
</form>
</body>
</html>
```

**cookie.java:**
```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class cookie extends HttpServlet {
    static int i = 1;
    
    public void doGet(HttpServletRequest req, HttpServletResponse res)
    throws IOException, ServletException {
        res.setContentType("text/html");
        PrintWriter out = res.getWriter();
        String k = String.valueOf(i);
        Cookie c = new Cookie("visit", k);
        res.addCookie(c);
        int j = Integer.parseInt(c.getValue());
        
        if(j == 1) {
            out.println("<h3>!!Welcome!! Now refresh your page</h3>");
        }
        else {
            out.println("<h3>You visited " + i + " times</h3>");
        }
        i++;
    }
}
```

### 🅒 Session Management

**Algorithm:** Demonstrate session creation, destruction and visit tracking.

**index.html:**
```html
<html>
<head>
<title>Using Session</title>
</head>
<body>
<form action="Session" method="get">
Enter User Id:<input type="text" name="txtName"><br><br>
<input type="submit" value="Submit">
<input type="reset" value="Reset">
</form>
</body>
</html>
```

**Session.java:**
```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class Session extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse res)
    throws IOException, ServletException {
        PrintWriter out = res.getWriter();
        out.println("<html><body>");
        HttpSession hs = req.getSession(true);
        
        if(hs.isNew()) {
            String name = req.getParameter("txtName");
            hs.setAttribute("uname", name);
            hs.setAttribute("visit", "1");
            out.println("<h2>Welcome First Time</h2>");
        }
        else {
            out.println("<h2>Welcome Again</h2>");
            int visit = Integer.parseInt((String)hs.getAttribute("visit")) + 1;
            out.println("<h2>You visited " + visit + " times</h2>");
            hs.setAttribute("visit", String.valueOf(visit));
        }
        
        out.println("<h2>Your Session Id " + hs.getId() + "</h2>");
        out.println("<h2>You Logged in at " + new java.util.Date(hs.getCreationTime()) + "</h2>");
        out.println("<h2><a href=logoutServlet>Click to LOGOUT</a></h2>");
        out.println("</body></html>");
    }
}
```

**logoutServlet.java:**
```java
import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.ServletException;
import javax.servlet.http.*;

public class logoutServlet extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse res)
    throws IOException, ServletException {
        PrintWriter out = res.getWriter();
        out.println("<html><body>");
        HttpSession hs = req.getSession();
        
        if(hs != null) {
            hs.invalidate();
        }
        
        out.println("<h1>You are logout now...</h1>");
        out.println("</body></html>");
    }
}
```

---

## PRACTICAL NO: 3
### **AIM**
Implement the Servlet IO and File applications.

### 🅐 File Upload and Download

**File Upload:**

**index.html:**
```html
<html>
<head>
<title>File_Upload</title>
</head>
<body>
<h2>File upload</h2>
Select the file to upload:<br>
<form action="uploadServlet" method="POST" enctype="multipart/form-data">
<input type="file" name="file" size="50" value="Choose File"><br><br>
<input type="submit" value="Upload File">
</form>
</body>
</html>
```

**uploadServlet.java:**
```java
import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import com.oreilly.servlet.MultipartRequest;

public class uploadServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
        PrintWriter out = response.getWriter();
        MultipartRequest m = new MultipartRequest(request, "D:\\");
        out.print("<html><body><h2>Successfully Uploaded</h2></body></html>");
    }
}
```

**File Download:**

**index.html:**
```html
<html>
<head>
<title>Download File</title>
</head>
<body>
<h2>File Download</h2>
<a href="download">Download the file</a>
</body>
</html>
```

**download.java:**
```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class download extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse res)
    throws IOException, ServletException {
        PrintWriter out = res.getWriter();
        String filename = "Practical3.txt";
        String filepath = "D:\\";
        
        res.setHeader("Content-Disposition", "attachment; filename=" + filename);
        FileInputStream f = new FileInputStream(filepath + filename);
        int i;
        while((i = f.read()) != -1) {
            out.write(i);
        }
        f.close();
    }
}
```

### 🅑 Question Answer Application

**Algorithm:** Create a simple quiz application with multiple choice questions.

**index.html:**
```html
<html>
<head>
<title>Question Answer Application</title>
</head>
<body>
<form method="post" action="checkServlet">
<h1>My paper</h1>

Q. 1) Which is a valid keyword in java?<br>
<input type="radio" name="r1" value="int"/>interface
<input type="radio" name="r1" value="F"/>Float
<input type="radio" name="r1" value="s"/>string
<input type="radio" name="r1" value="all"/>All of the above<br><br>

Q. 2) What is sent to the user via HTTP, invoked using the HTTP protocol on the user's computer, and run on the user's computer as an application?<br>
<input type="radio" name="r2" value="app"/>A Java application
<input type="radio" name="r2" value="applet"/>A Java applet
<input type="radio" name="r2" value="servlet"/>A Java servlet
<input type="radio" name="r2" value="none"/>None of the above<br><br>

Q. 3) JDBC stands for:<br>
<input type="radio" name="r3" value="jdbc"/>Java Database Connectivity
<input type="radio" name="r3" value="jdbc1"/>Java Database Components
<input type="radio" name="r3" value="jdbc2"/>Java Database Control
<input type="radio" name="r3" value="none"/>None of the above<br><br>

Q. 4) What is bytecode?<br>
<input type="radio" name="r4" value="msc"/>Machine-specific code
<input type="radio" name="r4" value="jcn"/>Java code
<input type="radio" name="r4" value="mic"/>Machine-independent code
<input type="radio" name="r4" value="none"/>None of the above<br><br>

<input type="submit" value="Display Result"/>
<input type="reset" value="Reset Values"/>
</form>
</body>
</html>
```

**checkServlet.java:**
```java
import java.io.*;
import javax.servlet.*;

public class checkServlet extends GenericServlet {
    public void service(ServletRequest req, ServletResponse res)
    throws ServletException, IOException {
        res.setContentType("text/html;charset=UTF-8");
        PrintWriter out = res.getWriter();
        
        try {
            out.println("<html>");
            out.println("<head>");
            out.println("<title>Servlet page</title>");
            out.println("</head>");
            out.println("<body>");
            
            String a1, a2, a3, a4;
            a1 = req.getParameter("r1");
            a2 = req.getParameter("r2");
            a3 = req.getParameter("r3");
            a4 = req.getParameter("r4");
            
            if((a1.equals("int")) && (a2.equals("applet")) && 
               (a3.equals("jdbc")) && (a4.equals("mic"))) {
                out.println("<h1>You are Pass</h1>");
            } else {
                out.println("<h1>Better luck Next time</h1>");
            }
            
            out.println("</body>");
            out.println("</html>");
        } finally {
            out.close();
        }
    }
}
```

---

## PRACTICAL NO: 4
### **AIM**
Implement the following JSP applications.

### 🅐 JSP Intrinsic Objects

**Algorithm:** Display values obtained from various JSP implicit objects.

**Implicit.jsp:**
```jsp
<html>
<body>
<h1>Use of implicit object in jsp</h1>

<h1>Request Object</h1>
Context Path <%=request.getContextPath()%><br>
Remote Host <%=request.getRemoteHost()%><br>

<h1>Response Object</h1>
Character Encoding Type <%=response.getCharacterEncoding()%><br>
Content Type <%=response.getContentType()%><br>

<h1>Session Object</h1>
ID <%=session.getId()%><br>
Creation Time <%=new java.util.Date(session.getCreationTime())%><br>
Last Access Time <%=new java.util.Date(session.getLastAccessedTime())%>
</body>
</html>
```

### 🅑 JSP Form Validation

**Algorithm:** Pass data from one JSP page to another with validations.

**Index.html:**
```html
<html>
<head>
<title>JSP Validation</title>
</head>
<body>
<form action="validate.jsp">
Enter Your Name<input type="text" name="name"><br>
Enter Your Age<input type="text" name="age"><br>
Select Hobbies: 
<input type="checkbox" name="hob" value="Singing">Singing
<input type="checkbox" name="hob" value="Reading">Reading Books
<input type="checkbox" name="hob" value="Football">Playing Football<br>
Enter E-mail:<input type="email" name="email"><br>
Select Gender: 
<input type="radio" name="gender" value="male">Male
<input type="radio" name="gender" value="female">Female
<input type="radio" name="gender" value="other">Other<br><br>
<input type="hidden" name="error" value="">
<input type="submit" value="Submit Form">
<input type="reset" value="Reset">
</form>
</body>
</html>
```

**CheckerBean.java:**
```java
package mypack;

public class CheckerBean {
    private String name, age, hob, email, gender, error;
    
    public CheckerBean() {
        error = "";
    }
    
    public void setName(String n) { name = n; }
    public void setAge(String a) { age = a; }
    public void setError(String e) { error = e; }
    
    public String getName() { return name; }
    public String getAge() { return age; }
    public String getError() { return error; }
    
    public boolean validate() {
        boolean res = true;
        if(name == null) {
            error += "<br>Enter First Name";
            res = false;
        }
        if(age == null) {
            error += "<br>Enter age";
            res = false;
        }
        if(age != null && age.length() > 2) {
            error += "<br>Age Invalid";
            res = false;
        }
        return res;
    }
}
```

**validate.jsp:**
```jsp
<%@page import="mypack.*;" %>
<jsp:useBean id="obj" scope="request" class="mypack.CheckerBean">
<jsp:setProperty name="obj" property="*"/>
</jsp:useBean>

<%
if (obj.validate()) {
%>
<jsp:forward page="Successful.jsp"/>
<%
} else {
%>
<jsp:include page="index.html"/>
<%
}
%>
<%= obj.getError() %>
```

**Successful.jsp:**
```jsp
<html>
<body>
<h1>DATA VALIDATED SUCCESSFULLY</h1>
<%
String s1 = request.getParameter("name");
out.print(s1);
%>
</body>
</html>
```

### 🅒 Registration and Login JSP with JDBC

**Algorithm:** Create registration and authentication system using JSP and JDBC.

**Index.html:**
```html
<html>
<head>
<title>JSP Registration</title>
</head>
<body>
<form action="Register.jsp">
<h1>New User Registration Page</h1>
Enter User Name <input type="text" name="txtName"><br>
Enter Password <input type="password" name="txtPass1"><br>
Re-Enter Password<input type="password" name="txtPass2"><br>
Enter Email<input type="text" name="txtEmail"><br>
Enter Country Name <input type="text" name="txtCon"><br><br>
<input type="submit" value="Register">
<input type="reset" value="Reset">
</form>
</body>
</html>
```

**Register.jsp:**
```jsp
<%@page contentType="text/html" import="java.sql.*"%>
<%
String uname = request.getParameter("txtName");
String pass1 = request.getParameter("txtPass1");
String pass2 = request.getParameter("txtPass2");
String email = request.getParameter("txtEmail");
String ctry = request.getParameter("txtCon");

if(pass1.equals(pass2)) {
    try {
        Class.forName("com.mysql.jdbc.Driver");
        Connection con = DriverManager.getConnection(
            "jdbc:mysql://localhost:3306/mydb","root","system");
        PreparedStatement stmt = con.prepareStatement("insert into user values(?,?,?,?)");
        stmt.setString(1, uname);
        stmt.setString(2, pass1);
        stmt.setString(3, email);
        stmt.setString(4, ctry);
        int row = stmt.executeUpdate();
        
        if(row == 1) {
            out.println("<h2>Registration Successful</h2>");
        }
        else {
            out.println("<h2>Registration FAILED!!!!</h2>");
        }
    }
    catch(Exception e) {
        out.println(e);
    }
}
else {
    out.println("<h2>Password Mismatch</h2>");
}
%>
```

---

## PRACTICAL NO: 5
### **AIM**
Implement the following JSP, JSTL and EL Applications.

### 🅐 Database Update using JSP

**Algorithm:** Update employee table in database based on employee number.

**index.html:**
```html
<html>
<head>
<title>JSP Employee</title>
</head>
<body>
<form action="Update.jsp">
Emp No.:<input type="text" name="t1"><br>
Emp Name:<input type="text" name="t2"><br>
Emp Age:<input type="text" name="t3"><br>
Emp Salary:<input type="text" name="t4"><br><br>
<input type="submit" value="Update">
<input type="reset" value="Reset">
</form>
</body>
</html>
```

**Update.jsp:**
```jsp
<%@page contentType="text/html" pageEncoding="UTF-8"%>
<%@page import="java.sql.*" %>
<%
String eno = request.getParameter("t1");
String ename = request.getParameter("t2");
String age = request.getParameter("t3");
String salary = request.getParameter("t4");

try {
    Class.forName("com.mysql.jdbc.Driver");
    Connection con = DriverManager.getConnection(
        "jdbc:mysql://localhost:3306/emp1","root","system");
    PreparedStatement stmt = con.prepareStatement("select * from tab where eno=?");
    stmt.setString(1, eno);
    ResultSet rs = stmt.executeQuery();
    
    if(rs.next()) {
        PreparedStatement pst1 = con.prepareStatement(
            "update tab set ename=?,age=?,salary=? where eno=?");
        pst1.setString(1, ename);
        pst1.setString(2, age);
        pst1.setString(3, salary);
        pst1.setString(4, eno);
        pst1.executeUpdate();
        out.print("<h1>Record updated</h1>");
    }
    else {
        out.print("<h1>Record not found</h1>");
    }
}
catch(Exception e) {
    out.print(e);
}
%>
```

### 🅑 Expression Language Demo

**Algorithm:** Demonstrate the use of Expression Language in JSP.

**Index.jsp:**
```jsp
<html>
<body>
<%
session.setAttribute("user", "Shubham");
Cookie s = new Cookie("name", "Shubh");
response.addCookie(s);
%>
<a href="Expression.jsp">Visit</a>
</body>
</html>
```

**Expression.jsp:**
```jsp
<html>
<body>
<h1>Use of Expression Language</h1><br>
${"Learning Expression"}<br>
Expression1: ${1>(4/2)}<br>
Expression2: ${(10*10) ne 100}<br>
<h1>Use of implicit object in Expression Language</h1><br>
Expression Language session Scope Object: ${sessionScope.user}<br>
Expression Language cookie: ${cookie.name.value}
</body>
</html>
```

### 🅒 JSTL Functions Demo

**Algorithm:** Demonstrate various JSTL functions for string manipulation.

**Function.jsp:**
```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<%@ taglib uri="http://java.sun.com/jsp/jstl/functions" prefix="fn" %>
<html>
<body>
<c:set var="String" value="Welcome-to-tutorials-point"/>
<h3>
contains: ${fn:contains(String,"tutorial")}<br>
indexOf: ${fn:indexOf(String,"to")}<br>
replace: ${fn:replace(String,"tutorials","javat")}<br>
toLowerCase: ${fn:toLowerCase(String)}<br>
toUpperCase: ${fn:toUpperCase(String)}<br>
substring: ${fn:substring(String,5,11)}<br>
substringAfter: ${fn:substringAfter(String,"to")}<br>
Length of the string is: ${fn:length(String)}
</h3>
</body>
</html>
```

---

## PRACTICAL NO: 6
### **AIM**
Implement the following EJB Applications.

### 🅐 Currency Converter using EJB

**Algorithm:** Create currency conversion application using Enterprise Java Beans.

**index.html:**
```html
<html>
<head>
<title>Currency Converter</title>
</head>
<body>
<form action="CCServlet">
Enter Amount:<input type="text" name="amt"><br>
Select Conversion Type:
<input type="radio" name="type" value="r2d" checked>Rupees to Dollar
<input type="radio" name="type" value="d2r">Dollar to Rupees<br><br>
<input type="submit" value="CONVERT">
<input type="reset" value="RESET">
</form>
</body>
</html>
```

**CCBean.java:**
```java
package mybean;
import javax.ejb.Stateless;

@Stateless
public class CCBean {
    
    public CCBean() {
    }
    
    public double r2Dollar(double r) {
        return r / 83.99;
    }
    
    public double d2Rupees(double d) {
        return d * 83.99;
    }
}
```

**CCServlet.java:**
```java
import mybean.CCBean;
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import javax.ejb.EJB;

public class CCServlet extends HttpServlet {
    @EJB CCBean obj;
    
    public void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
        response.setContentType("text/html;charset=UTF-8");
        PrintWriter out = response.getWriter();
        double amt = Double.parseDouble(request.getParameter("amt"));
        
        if(request.getParameter("type").equals("r2d")) {
            out.println("<h1>" + amt + " Rupees = " + obj.r2Dollar(amt) + " Dollars</h1>");
        }
        if(request.getParameter("type").equals("d2r")) {
            out.println("<h1>" + amt + " Dollars = " + obj.d2Rupees(amt) + " Rupees</h1>");
        }
    }
}
```

### 🅑 Room Reservation System using EJB

**Algorithm:** Develop hotel room reservation system using EJB.

**index.html:**
```html
<html>
<head>
<title>The Presidential Hotel</title>
</head>
<body>
<h1>Enter the Details for Room Reservation</h1><br>
<form action="Reserver" method="POST">
Enter Your Name:<input type="text" name="tname"><br>
Enter Your Address:<input type="text" name="tadd"><br>
Enter Your Phone Number:<input type="text" name="tphone"><br>
Enter Room Type:<select name="troom">
<option id="g">GENERAL</option>
<option id="d">DELUXE</option>
<option id="s">SUITE</option>
</select><br>
Enter CheckIn Date: <input type="text" name="tin"><br>
Enter CheckOut Date:<input type="text" name="tout"><br>
Enter Payment Mode:<select name="tpay">
<option id="c">CASH</option>
<option id="e">CREDIT CARD</option>
</select><br><br>
<input type="submit" value="SUBMIT">
<input type="reset" value="RESET">
</form>
</body>
</html>
```

**Reserver.java:**
```java
import ejb.Details;
import java.io.*;
import java.util.ArrayList;
import javax.servlet.*;
import javax.servlet.http.*;
import javax.ejb.EJB;

public class Reserver extends HttpServlet {
    Details d = new Details();
    
    protected void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
        PrintWriter out = response.getWriter();
        String cname = request.getParameter("tname");
        String cadd = request.getParameter("tadd");
        String cph = request.getParameter("tphone");
        String croom = request.getParameter("troom");
        String chin = request.getParameter("tin");
        String chout = request.getParameter("tout");
        String cmode = request.getParameter("tpay");
        
        ArrayList<String> a = d.reserve(cname, cadd, cph, croom, chin, chout, cmode);
        out.println("<html><body><h2>");
        
        try {
            out.println(d.welmsg(cname) + "<br>");
            out.println(d.rtype(croom) + "<br>");
            out.println(d.roompay(croom) + "<br>");
            out.println("<br>----Your Details----<br>");
            out.println("<table border=1><tr><th>Name</th><th>Address</th><th>PhoneNo.</th>" +
                       "<th>RoomType</th><th>CheckIn Date</th><th>CheckOut Date</th><th>Payment Mode</th></tr>");
            out.println("<tr>");
            
            for(int i = 0; i < 7; i++) {
                out.println("<td>" + a.get(i) + "</td>");
            }
            out.println("</tr></table>");
        }
        catch(Exception e) {
            out.println(e);
        }
        out.println("</h2></body></html>");
    }
}
```

**Details.java:**
```java
package ejb;
import java.util.ArrayList;

public class Details {
    
    public String welmsg(String cust) {
        return "Hello " + cust.toUpperCase() + " <br>Welcome to The Presidential Hotel";
    }
    
    public String rtype(String rt) {
        return "You Have Selected " + rt.toUpperCase() + " Room";
    }
    
    public String roompay(String rt) {
        if(rt.equalsIgnoreCase("SUITE")) {
            return "You have To Pay 8000Rs Only";
        }
        else if(rt.equalsIgnoreCase("DELUXE")) {
            return "You have To Pay 4000Rs Only";
        }
        else {
            return "You Have To Pay 2000Rs Only";
        }
    }
    
    public ArrayList<String> reserve(String cust, String add, String ph, 
                                   String rt1, String checkin, String checkout, String pyr) {
        ArrayList<String> a = new ArrayList();
        a.add(cust);
        a.add(add);
        a.add(ph);
        a.add(rt1);
        a.add(checkin);
        a.add(checkout);
        a.add(pyr);
        return a;
    }
}
```

---

## PRACTICAL NO: 7
### **AIM**
Implement the following EJB Applications with different types of Beans.

### 🅐 Servlet Hit Counter using Singleton Session Beans

**Algorithm:** Track servlet access count using Singleton EJB.

**index.html:**
```html
<html>
<head>
<meta http-equiv="Refresh" content="0; URL=ServletClient">
</head>
</html>
```

**ServletClient.java:**
```java
import ejb.HitsBean;
import java.io.IOException;
import java.io.PrintWriter;
import javax.ejb.EJB;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class ServletClient extends HttpServlet {
    @EJB
    HitsBean counter;
    
    protected void doGet(HttpServletRequest req, HttpServletResponse res) 
    throws IOException {
        PrintWriter out = res.getWriter();
        try {
            out.print("<h1>Number of times this servlet is accessed: </h1>" + counter.getHitCnt());
        }
        finally {
            out.close();
        }
    }
}
```

**HitsBean.java:**
```java
package ejb;
import javax.ejb.Singleton;

@Singleton
public class HitsBean {
    private int hitcnt;
    
    public int getHitCnt() {
        return hitcnt++;
    }
}
```

### 🅑 Marks Entry Application with Database Access

**Algorithm:** Store student marks in database using EJB.

**index.html:**
```html
<html>
<head>
<title>Marks Entry Application</title>
</head>
<body>
<form action="MarkEntrySrv" method="get">
Enter Roll No.:<input type="text" name="srno"><br>
Enter Student Name:<input type="text" name="name"><br>
Enter Marks(EJ):<input type="text" name="m1"><br>
Enter marks(AWP):<input type="text" name="m2"><br><br>
<input type="submit" value="Submit">
<input type="reset" value="Reset">
</form>
</body>
</html>
```

**MarkEntrySrv.java:**
```java
import ejb.MarksEntry;
import java.io.*;
import javax.ejb.EJB;
import javax.servlet.*;
import javax.servlet.http.*;

public class MarkEntrySrv extends HttpServlet {
    @EJB
    MarksEntry bean;
    
    public void doGet(HttpServletRequest req, HttpServletResponse res)
    throws IOException, ServletException {
        PrintWriter out = res.getWriter();
        String id, name, p1, p2;
        id = req.getParameter("srno");
        name = req.getParameter("name");
        p1 = req.getParameter("m1");
        p2 = req.getParameter("m2");
        
        bean.entry(id, name, p1, p2);
        out.print(bean.submit(name));
    }
}
```

**MarksEntry.java:**
```java
package ejb;
import java.sql.*;
import javax.ejb.Stateless;

@Stateless
public class MarksEntry {
    
    public void entry(String srno, String sname, String p1, String p2) {
        try {
            Class.forName("com.mysql.jdbc.Driver");
            Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/mysql","root","system");
            PreparedStatement ps = con.prepareStatement("insert into student values(?,?,?,?)");
            ps.setString(1, srno);
            ps.setString(2, sname);
            ps.setString(3, p1);
            ps.setString(4, p2);
            ps.executeUpdate();
        }
        catch(Exception e) {
            System.out.print(e);
        }
    }
    
    public String submit(String name) {
        return("<h1>" + name.toUpperCase() + "<br>Record submitted successfully!!</h1>");
    }
}
```







*Powered by Ajay! 🎯*
