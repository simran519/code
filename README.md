# AWD PRACTICALS

## PRACTICAL NO: 1





### 🅑Create an application to print on screen the output of adding, subtracting, multiplying, and dividing two numbers entered by the user in C#.

**Calculator:**

**WebForm1.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="practical1a.WebForm1" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Arithmetic Operations</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:Label ID="Label5" runat="server" Text="Enter Number 1:"></asp:Label>
            <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox><br /><br />

            <asp:Label ID="Label6" runat="server" Text="Enter Number 2:"></asp:Label>
            <asp:TextBox ID="TextBox2" runat="server"></asp:TextBox><br /><br />

            <asp:Button ID="Button1" runat="server" Text="Results" OnClick="Button1_Click" /><br /><br />

            <asp:Label ID="Label1" runat="server" Text="Addition is : "></asp:Label><br />
            <asp:Label ID="Label2" runat="server" Text="Subtraction is : "></asp:Label><br />
            <asp:Label ID="Label3" runat="server" Text="Multiplication is : "></asp:Label><br />
            <asp:Label ID="Label4" runat="server" Text="Division is : "></asp:Label>
        </div>
    </form>
</body>
</html>

```


**WebForm1.aspx.cs:**
```
using System;
using System.Web.UI;

namespace practical1a
{
    public partial class WebForm1 : Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void Button1_Click(object sender, EventArgs e)
        {
            int num1 = Convert.ToInt32(TextBox1.Text);
            int num2 = Convert.ToInt32(TextBox2.Text);

            int addition = num1 + num2;
            int subtraction = num1 - num2;
            int multiplication = num1 * num2;
            int division = num1 / num2;

            Label1.Text = "Addition of the numbers is: " + addition;
            Label2.Text = "Subtraction of the numbers is: " + subtraction;
            Label3.Text = "Multiplication of the numbers is: " + multiplication;
            Label4.Text = "Division of the numbers is: " + division;
        }
    }
}


```

### 🅑Create a simple application to demonstrate the concepts boxing and unboxing.



**Boxing & Unboxing:**

**WebForm1.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="practical2a.WebForm1" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Boxing and Unboxing</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:Label ID="Label1" runat="server" Text="Enter a Number:"></asp:Label>
            <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
            <br /><br />
            <asp:Button ID="Button1" runat="server" Text="Show Boxed and Unboxed Values" OnClick="Button1_Click" />
            <br /><br />
            <asp:Label ID="Label2" runat="server" Text=""></asp:Label><br />
            <asp:Label ID="Label3" runat="server" Text=""></asp:Label>
        </div>
    </form>
</body>
</html>


```

**WebForm1.aspx.cs:**
```
using System;
using System.Web.UI;

namespace practical2a
{
    public partial class WebForm1 : Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void Button1_Click(object sender, EventArgs e)
        {
            int valueType = Convert.ToInt32(TextBox1.Text);

            // Boxing
            object boxed = valueType;
            Label2.Text = "Boxed Value: " + boxed;

            // Unboxing
            int unboxed = (int)boxed;
            Label3.Text = "Unboxed Value: " + unboxed;
        }
    }
}


```

### 🅒 Create a simple application to demonstrate use of the concepts of interfaces. 


**Interface:**

**WebForm1.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="practical2c.WebForm1" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Interface Example</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <h2>Area Calculation using Interface</h2>
            <asp:Label ID="Label1" runat="server" Text="Area of Circle: "></asp:Label>
            <asp:Label ID="Label2" runat="server" Text=""></asp:Label>
            <br /><br />
            <asp:Label ID="Label3" runat="server" Text="Area of Rectangle: "></asp:Label>
            <asp:Label ID="Label4" runat="server" Text=""></asp:Label>
        </div>
    </form>
</body>
</html>



```

**WebForm1.aspx.cs:**
```
using System;
using System.Web.UI;

namespace practical2c
{
    interface Area
    {
        double Show(double a, double b);
    }

    class Rectangle : Area
    {
        public double Show(double a, double b)
        {
            return a * b;
        }
    }

    class Circle : Area
    {
        public double Show(double a, double b)
        {
            return 3.14 * a * a;
        }
    }

    public partial class WebForm1 : Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            Circle cir = new Circle();
            Rectangle rect = new Rectangle();

            double circleArea = cir.Show(3, 0);     // 3 is radius
            double rectArea = rect.Show(5, 4);      // 5×4 rectangle

            Label2.Text = circleArea.ToString();    // circle label
            Label4.Text = rectArea.ToString();      // rectangle label
        }
    }
}



```

### 🅒Create a simple web page with various server controls to demonstrate setting and use of their properties. (Example :AutoPostBack)


**AutoPostBack:**

**WebForm1.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="practical3a.WebForm1" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head1" runat="server">
    <title>AutoPostBack Example</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <h2>Demonstrate AutoPostBack Property</h2>

            <asp:Label ID="Label1" runat="server" Text="Enter Your Name:"></asp:Label>
            <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
            <br /><br />

            <asp:Label ID="Label2" runat="server" Text="Select Your City:"></asp:Label>
            <asp:DropDownList ID="DropDownList1" runat="server" AutoPostBack="True" OnSelectedIndexChanged="DropDownList1_SelectedIndexChanged">
                <asp:ListItem>--Select--</asp:ListItem>
                <asp:ListItem>Mumbai</asp:ListItem>
                <asp:ListItem>Pune</asp:ListItem>
                <asp:ListItem>Nagpur</asp:ListItem>
                <asp:ListItem>Nashik</asp:ListItem>
            </asp:DropDownList>

            <br /><br />
            <asp:Label ID="Label3" runat="server" Text=""></asp:Label>
        </div>
    </form>
</body>
</html>



```

**WebForm1.aspx.cs:**
```
using System;
using System.Web.UI;

namespace practical3a
{
    public partial class WebForm1 : Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void DropDownList1_SelectedIndexChanged(object sender, EventArgs e)
        {
            string name = TextBox1.Text;
            string city = DropDownList1.SelectedItem.Text;

            if (city != "--Select--" && name != "")
                Label3.Text = "Hello " + name + ", You are from " + city + ".";
            else
                Label3.Text = "";
        }
    }
}



```


### 🅒Demonstrate the use of Treeview operations on the web form.


**TreeView:**

**student.xml:**
```
<?xml version="1.0" encoding="utf-8"?>
<Students>
  <Student Name="Sachin">
    <Course>BSc IT</Course>
    <City>Mumbai</City>
  </Student>
  <Student Name="Amit">
    <Course>BSc CS</Course>
    <City>Pune</City>
  </Student>
  <Student Name="Riya">
    <Course>BCA</Course>
    <City>Nagpur</City>
  </Student>
</Students>



```

**WebForm1.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true"
    CodeBehind="WebForm1.aspx.cs"
    Inherits="practical3d.WebForm1" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head1" runat="server">
    <title>TreeView using XMLDataSource</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <h2>Display Student Details using TreeView Control</h2>

            <asp:XmlDataSource ID="XmlDataSource1" runat="server" DataFile="~/Student.xml" />

            <asp:TreeView ID="TreeView1" runat="server" DataSourceID="XmlDataSource1">
            </asp:TreeView>
        </div>
    </form>
</body>
</html>
```


**WebForm1.aspx.cs:**
```
using System;
using System.Web.UI;

namespace practical3d
{
    public partial class WebForm1 : Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }
    }
}


```

### 🅒Create a Registration form to demonstrate use of various Validation controls.

**1.  Range Validator:**

**WebForm1.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="practical4a.WebForm1" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head1" runat="server">
    <title>RangeValidator Example</title>
</head>
<body>
    <form id="form1" runat="server">
        <div style="text-align:center">
            <h2>RangeValidator Control Example</h2>

            <asp:Label ID="Label1" runat="server" Text="Enter your Age: "></asp:Label>
            <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>

            <asp:RangeValidator ID="RangeValidator1" runat="server"
                ControlToValidate="TextBox1"
                MinimumValue="18" MaximumValue="30"
                Type="Integer"
                ErrorMessage="Age must be between 18 and 30"
                ForeColor="Red">*</asp:RangeValidator>

            <br /><br />

            <asp:Button ID="Button1" runat="server" Text="Submit" OnClick="Button1_Click" />

            <br /><br />
            <asp:Label ID="Label2" runat="server" ForeColor="Green"></asp:Label>
        </div>
    </form>
</body>
</html>



```

**WebForm1.aspx.cs:**
```
using System;
using System.Web.UI;

namespace practical4a
{
    public partial class WebForm1 : Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void Button1_Click(object sender, EventArgs e)
        {
            if (Page.IsValid)
            {
                Label2.Text = "Age Accepted!";
            }
            else
            {
                Label2.Text = "";
            }
        }
    }
}



```

**Web.config:**
```
<?xml version="1.0"?>
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.0" />
    <pages validateRequest="true" />
  </system.web>
</configuration>



```


**2.  Compare Validator:**

**WebForm1.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="practical4a.WebForm1" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head1" runat="server">
    <title>CompareValidator Example</title>
</head>
<body>
    <form id="form1" runat="server">
        <div style="text-align:center">
            <h2>CompareValidator Control Example</h2>

            <asp:Label ID="Label1" runat="server" Text="Enter Password: "></asp:Label>
            <asp:TextBox ID="TextBox1" runat="server" TextMode="Password"></asp:TextBox>

            <br /><br />

            <asp:Label ID="Label2" runat="server" Text="Confirm Password: "></asp:Label>
            <asp:TextBox ID="TextBox2" runat="server" TextMode="Password"></asp:TextBox>

            <asp:CompareValidator ID="CompareValidator1" runat="server"
                ControlToCompare="TextBox1"
                ControlToValidate="TextBox2"
                ErrorMessage="Passwords do not match!"
                ForeColor="Red">*</asp:CompareValidator>

            <br /><br />

            <asp:Button ID="Button1" runat="server" Text="Submit" OnClick="Button1_Click" />

            <br /><br />
            <asp:Label ID="Label3" runat="server" ForeColor="Green"></asp:Label>
        </div>
    </form>
</body>
</html>



```

**WebForm1.aspx.cs:**
```
using System;
using System.Web.UI;

namespace practical4a
{
    public partial class WebForm1 : Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void Button1_Click(object sender, EventArgs e)
        {
            if (Page.IsValid)
            {
                Label3.Text = "Password Matched!";
            }
            else
            {
                Label3.Text = "";
            }
        }
    }
}



```

**Web.config:**
```
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.0" />
    <pages validateRequest="true" />
  </system.web>

  <system.webServer>
    <defaultDocument>
      <files>
        <add value="WebForm1.aspx" />
      </files>
    </defaultDocument>
  </system.webServer>
</configuration>



```


**3. RequiredFieldValidator:**

**WebForm1.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="practical4a.WebForm1" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head1" runat="server">
    <title>RequiredFieldValidator Example</title>
</head>
<body>
    <form id="form1" runat="server">
        <div style="text-align:center">
            <h2>RequiredFieldValidator Control Example</h2>

            <asp:Label ID="Label1" runat="server" Text="Enter Your Name: "></asp:Label>
            <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>

            <asp:RequiredFieldValidator ID="RequiredFieldValidator1" runat="server"
                ControlToValidate="TextBox1"
                ErrorMessage="Name is required!"
                ForeColor="Red">*</asp:RequiredFieldValidator>

            <br /><br />

            <asp:Button ID="Button1" runat="server" Text="Submit" OnClick="Button1_Click" />

            <br /><br />
            <asp:Label ID="Label2" runat="server" ForeColor="Green"></asp:Label>
        </div>
    </form>
</body>
</html>



```

**WebForm1.aspx.cs:**
```
using System;
using System.Web.UI;

namespace practical4a
{
    public partial class WebForm1 : Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void Button1_Click(object sender, EventArgs e)
        {
            if (Page.IsValid)
            {
                Label2.Text = "Name Submitted Successfully!";
            }
            else
            {
                Label2.Text = "";
            }
        }
    }
}


```

**Web.config:**
```
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.0" />
    <pages validateRequest="true" />
  </system.web>

  <system.webServer>
    <defaultDocument>
      <files>
        <add value="WebForm1.aspx" />
      </files>
    </defaultDocument>
  </system.webServer>
</configuration>




```


**4. RegularExpressionValidator:**

**WebForm1.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="practical4a.WebForm1" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>RegularExpressionValidator Example</title>
</head>
<body>
    <form id="form1" runat="server">
        <div style="text-align:center">
            <h2>RegularExpressionValidator Control Example</h2>

            <asp:Label ID="Label1" runat="server" Text="Enter Email ID: "></asp:Label>
            <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>

            <asp:RegularExpressionValidator ID="RegularExpressionValidator1" runat="server"
                ControlToValidate="TextBox1"
                ErrorMessage="Enter a valid Email ID!"
                ValidationExpression="\w+([-+.']\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*"
                ForeColor="Red">*</asp:RegularExpressionValidator>

            <br /><br />

            <asp:Button ID="Button1" runat="server" Text="Submit" OnClick="Button1_Click" />

            <br /><br />
            <asp:Label ID="Label2" runat="server" ForeColor="Green"></asp:Label>
        </div>
    </form>
</body>
</html>




```

**WebForm1.aspx.cs:**
```
using System;
using System.Web.UI;

namespace practical4a
{
    public partial class WebForm1 : Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void Button1_Click(object sender, EventArgs e)
        {
            if (Page.IsValid)
            {
                Label2.Text = "Valid Email ID!";
            }
            else
            {
                Label2.Text = "";
            }
        }
    }
}





```

**Web.config:**
```
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.0" />
    <pages validateRequest="true" />
  </system.web>

  <system.webServer>
    <defaultDocument>
      <files>
        <add value="WebForm1.aspx" />
      </files>
    </defaultDocument>
  </system.webServer>
</configuration>




```


**5. CustomValidator:**

**WebForm1.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="practical4a.WebForm1" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>CustomValidator Example</title>
</head>
<body>
    <form id="form1" runat="server">
        <div style="text-align:center">
            <h2>CustomValidator Control Example</h2>

            <asp:Label ID="Label1" runat="server" Text="Enter a Number: "></asp:Label>
            <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>

            <asp:CustomValidator ID="CustomValidator1" runat="server"
                ControlToValidate="TextBox1"
                ErrorMessage="Enter an even number only!"
                OnServerValidate="CustomValidator1_ServerValidate"
                ForeColor="Red">*</asp:CustomValidator>

            <br /><br />

            <asp:Button ID="Button1" runat="server" Text="Submit" OnClick="Button1_Click" />

            <br /><br />
            <asp:Label ID="Label2" runat="server" ForeColor="Green"></asp:Label>
        </div>
    </form>
</body>
</html>


```

**WebForm1.aspx.cs:**
```
using System;
using System.Web.UI;

namespace practical4a
{
    public partial class WebForm1 : Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void CustomValidator1_ServerValidate(object source, ServerValidateEventArgs args)
        {
            int num;
            if (int.TryParse(args.Value, out num) && num % 2 == 0)
            {
                args.IsValid = true;
            }
            else
            {
                args.IsValid = false;
            }
        }

        protected void Button1_Click(object sender, EventArgs e)
        {
            if (Page.IsValid)
            {
                Label2.Text = "Valid Input!";
            }
            else
            {
                Label2.Text = "";
            }
        }
    }
}




```

**Web.config:**
```
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.0" />
    <pages validateRequest="true" />
  </system.web>

  <system.webServer>
    <defaultDocument>
      <files>
        <add value="WebForm1.aspx" />
      </files>
    </defaultDocument>
  </system.webServer>
</configuration>




```


### 🅒 Create Web Form to demonstrate use of Adrotator Control. 

**1.  AD Rotator:**

**AdFile.xml:**
```
<?xml version="1.0" encoding="utf-8"?>
<Advertisements>
  <Ad>
    <ImageUrl>~/Images/ad1.jpg</ImageUrl>
    <NavigateUrl>https://www.microsoft.com</NavigateUrl>
    <AlternateText>Visit Microsoft</AlternateText>
    <Impressions>3</Impressions>
  </Ad>
  <Ad>
    <ImageUrl>~/Images/ad2.jpg</ImageUrl>
    <NavigateUrl>https://www.google.com</NavigateUrl>
    <AlternateText>Visit Google</AlternateText>
    <Impressions>2</Impressions>
  </Ad>
  <Ad>
    <ImageUrl>~/Images/ad3.jpg</ImageUrl>
    <NavigateUrl>https://www.yahoo.com</NavigateUrl>
    <AlternateText>Visit Yahoo</AlternateText>
    <Impressions>1</Impressions>
  </Ad>
</Advertisements>

```

**WebForm1.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="practical4b.WebForm1" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head1" runat="server">
    <title>AdRotator Example</title>
</head>
<body>
<form id="form1" runat="server">
    <div style="text-align:center">
        <h2>AdRotator Control Example</h2>

        <asp:AdRotator ID="AdRotator1" runat="server"
            AdvertisementFile="~/AdFile.xml"
            Target="_blank" />
    </div>
</form>
</body>
</html>




```

**WebForm1.aspx.cs:**
```
using System;
using System.Web.UI;

namespace practical4b
{
    public partial class WebForm1 : Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }
    }
}



```

### 🅒  Create Web Form to demonstrate use User Controls.

**User Control:**

**Default.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" 
Inherits="_Default" %> 
<!DOCTYPE html> 
<html xmlns="http://www.w3.org/1999/xhtml"> 
<head runat="server"> 
<title></title> 
</head> 
<body> 
<form id="form1" runat="server"> 
<div> 
<asp:Label ID="Label1" runat="server" Text="This is User Control" Font-Bold="True" Font- 
Size="XX-Large" Font-Underline="True"></asp:Label> 
<br /><br /> 
<asp:Label ID="Label2" runat="server" Text="Name: "></asp:Label> 
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox> 
</div> 
<asp:Label ID="Label3" runat="server" Text="City: "></asp:Label> 
<asp:TextBox ID="TextBox2" runat="server"></asp:TextBox> 
<p> 
<asp:Button ID="Button1" runat="server" Text="Save" OnClick="Button1_Click" 
/></p><p> 
<asp:Label ID="Label4" runat="server" Text="Result:"></asp:Label>
</p> 
</form> 
</body> 
</html>

```

**Default.aspx.cs:**
```
using System; 
using System.Collections.Generic; 
using System.Linq; using 
System.Web; using System.Web.UI; 
using System.Web.UI.WebControls; 
public partial class _Default :System.Web.UI.Page{ 
protected void Page_Load(object sender, EventArgs e) 
{ 
} 
protected void Button1_Click(object sender, EventArgs e)  { 
Label4.Text += "</br>Your name is " + TextBox1.Text + "</br>You are from " + 
TextBox2.Text; 
}} 




```
### 🅒 Create Web Form to demonstrate use of Website Navigation controls.

**Site Map:**

**Home.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Home.aspx.cs" Inherits="practical4d.Home" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Home Page</title>
</head>
<body>
    <form id="form1" runat="server">
        <div style="text-align:center">

            <h2>Website Navigation Example</h2>
            <hr />

            <asp:SiteMapPath ID="SiteMapPath1" runat="server" />
            <br /><br />

            <asp:Menu ID="Menu1" runat="server" DataSourceID="SiteMapDataSource1"
                      Orientation="Horizontal" BackColor="#99CCFF"
                      Font-Bold="True" ForeColor="Black" />
            <br /><br />

            <asp:TreeView ID="TreeView1" runat="server"
                          DataSourceID="SiteMapDataSource1" />
            <asp:SiteMapDataSource ID="SiteMapDataSource1" runat="server" />

            <br /><br />
            <asp:Label ID="Label1" runat="server" Text="Welcome to the Home Page!" Font-Bold="True" />
        </div>
    </form>
</body>
</html>


```

**Home.aspx.cs:**
```
using System;
using System.Web.UI;

namespace practical4d
{
    public partial class Home : Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }
    }
}

```

**AboutUs.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="AboutUs.aspx.cs" Inherits="practical4d.AboutUs" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>About Us</title>
</head>
<body>
    <form id="form1" runat="server">
        <div style="text-align:center">
            <asp:SiteMapPath ID="SiteMapPath1" runat="server" />
            <h2>About Us Page</h2>
            <p>We are demonstrating Navigation Controls in ASP.NET.</p>
        </div>
    </form>
</body>
</html>




```

**AboutUs.aspx.cs:**
```
using System;
using System.Web.UI;

namespace practical4d
{
    public partial class AboutUs : Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }
    }
}

```

**ContactUs.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="ContactUs.aspx.cs" Inherits="practical4d.ContactUs" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Contact Us</title>
</head>
<body>
    <form id="form1" runat="server">
        <div style="text-align:center">
            <asp:SiteMapPath ID="SiteMapPath1" runat="server" />
            <h2>Contact Us Page</h2>
            <p>Email: info@example.com<br />Phone: 9876543210</p>
        </div>
    </form>
</body>
</html>


```

**ContactUs.aspx.cs:**
```
using System;
using System.Web.UI;

namespace practical4d
{
    public partial class ContactUs : Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }
    }
}



```

**Web.sitemap:**
```
<?xml version="1.0" encoding="utf-8"?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0">
  <siteMapNode title="Home" url="Home.aspx">
    <siteMapNode title="About Us" url="AboutUs.aspx" />
    <siteMapNode title="Contact Us" url="ContactUs.aspx" />
  </siteMapNode>
</siteMap>


```


**Web.config:**
```
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.0" />
    <siteMap defaultProvider="XmlSiteMapProvider" enabled="true">
      <providers>
        <add name="XmlSiteMapProvider"
             type="System.Web.XmlSiteMapProvider"
             siteMapFile="Web.sitemap" />
      </providers>
    </siteMap>
  </system.web>

  <system.webServer>
    <defaultDocument>
      <files>
        <add value="Home.aspx" />
      </files>
    </defaultDocument>
  </system.webServer>
</configuration>

```

### 🅒 Create a web application to demonstrate use of Master Page and content page.

**Master Page:**

**MasterPage.master:**
```
<%@ Master Language="C#" AutoEventWireup="true" CodeFile="MasterPage.master.cs" Inherits="SiteMaster" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head1" runat="server">
    <title>Master Page Example</title>
    <asp:ContentPlaceHolder ID="head" runat="server"></asp:ContentPlaceHolder>
</head>
<body>
    <form id="form1" runat="server">
        <div style="text-align:center">
            <asp:ContentPlaceHolder ID="ContentPlaceHolder1" runat="server"></asp:ContentPlaceHolder>
            <br />
            <asp:ContentPlaceHolder ID="ContentPlaceHolder2" runat="server"></asp:ContentPlaceHolder>
            <br />
 <asp:ContentPlaceHolder ID="ContentPlaceHolder3" runat="server"></asp:ContentPlaceHolder>
        </div>
    </form>
</body>
</html>

```

**MasterPage.master.cs:**
```
using System;
using System.Web.UI;

public partial class SiteMaster : MasterPage
{
    protected void Page_Load(object sender, EventArgs e)
    {
    }
}
```

**Default.aspx:**
```
<%@ Page Language="C#" MasterPageFile="~/MasterPage.master"
    AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<asp:Content ID="Content1" ContentPlaceHolderID="head" runat="server">
</asp:Content>

<asp:Content ID="Content2" ContentPlaceHolderID="ContentPlaceHolder1" runat="server">
    <asp:Label ID="Label1" runat="server" Text="Advanced Web Development"></asp:Label>
    <br />
</asp:Content>

<asp:Content ID="Content3" ContentPlaceHolderID="ContentPlaceHolder2" runat="server">
    <asp:Label ID="Label2" runat="server" Text="Advanced Java Technologies"></asp:Label>
    <br />
</asp:Content>
<asp:Content ID="Content4" ContentPlaceHolderID="ContentPlaceHolder3" runat="server">
    <asp:Button ID="Button1" runat="server" Text="Click Here" OnClick="Button1_Click" />
</asp:Content>




```

**Default.aspx.cs:**
```

using System;
using System.Web.UI;

public partial class _Default : Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
    }

    protected void Button1_Click(object sender, EventArgs e)
    {
        Label1.Text = "Artificial Intelligence & Applications";
        Label2.Text = "Software Project Development";
    }
}


```

### 🅒 Create a web application for inserting and deleting records from a database.

**DATABASE:**

**Default.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" 
Inherits="_Default" %>
<!DOCTYPE html> 
<html xmlns="http://www.w3.org/1999/xhtml"> 
<head runat="server"> 
<title></title> 
</head> 
<body> 
<form id="form1" runat="server"> 
<div> 
 
</div> 
<asp:DetailsView ID="DetailsView1" runat="server" AutoGenerateRows="False" 
DataKeyNames="Id" DataSourceID="SqlDataSource1" Height="50px" Width="125px"> 
<Fields> 
<asp:BoundField DataField="Id" HeaderText="Id" ReadOnly="True" SortExpression="Id" /> 
<asp:BoundField DataField="FirstName" HeaderText="FirstName" 
SortExpression="FirstName" /> 
<asp:BoundField DataField="LastName" HeaderText="LastName" 
SortExpression="LastName" /> 
<asp:BoundField DataField="City" HeaderText="City" SortExpression="City" /> 
<asp:BoundField DataField="Country" HeaderText="Country" SortExpression="Country" /> 
<asp:BoundField DataField="Phone" HeaderText="Phone" SortExpression="Phone" /> 
<asp:CommandField ShowDeleteButton="True" ShowInsertButton="True" /> 
</Fields> 
</asp:DetailsView> 
<asp:SqlDataSource ID="SqlDataSource1" runat="server" 
ConflictDetection="CompareAllValues" ConnectionString="<%$ 
ConnectionStrings:ConnectionString %>" DeleteCommand="DELETE FROM [Student] WHERE 
[Id] = @original_Id AND (([FirstName] = @original_FirstName) OR ([FirstName] IS NULL AND 
@original_FirstName IS NULL)) AND (([LastName] = @original_LastName) OR ([LastName] IS 
NULL AND @original_LastName IS NULL)) AND (([City] = @original_City) OR ([City] IS 
NULL AND @original_City IS NULL)) AND (([Country] = @original_Country) OR ([Country] IS 
NULL AND @original_Country IS NULL)) AND (([Phone] = @original_Phone) OR ([Phone] IS 
NULL AND @original_Phone IS NULL))" InsertCommand="INSERT INTO [Student] ([Id], 
[FirstName], [LastName], [City], [Country], [Phone]) VALUES (@Id, @FirstName, @LastName, 
@City, @Country, @Phone)" OldValuesParameterFormatString="original_{0}" 
SelectCommand="SELECT * FROM [Student]" UpdateCommand="UPDATE [Student] SET 
[FirstName] = @FirstName, [LastName] = @LastName, [City] = @City, [Country] = @Country, 
[Phone] = @Phone WHERE [Id] = @original_Id AND (([FirstName] = @original_FirstName) OR 
([FirstName] IS NULL AND @original_FirstName IS NULL)) AND (([LastName] = 
@original_LastName) OR ([LastName] IS NULL AND @original_LastName IS NULL)) AND 
(([City] = @original_City) OR ([City] IS NULL AND @original_City IS NULL)) AND (([Country]
= @original_Country) OR ([Country] IS NULL AND @original_Country IS NULL)) AND 
(([Phone] = @original_Phone) OR ([Phone] IS NULL AND @original_Phone IS NULL))"> 
<DeleteParameters> 
<asp:Parameter Name="original_Id" Type="Int32" /> 
<asp:Parameter Name="original_FirstName" Type="String" /> 
<asp:Parameter Name="original_LastName" Type="String" /> 
<asp:Parameter Name="original_City" Type="String" /> 
<asp:Parameter Name="original_Country" Type="String" />
<asp:Parameter Name="original_Phone" Type="String" /> 
</DeleteParameters> 
<InsertParameters> 
<asp:Parameter Name="Id" Type="Int32" /> 
<asp:Parameter Name="FirstName" Type="String" /> 
<asp:Parameter Name="LastName" Type="String" /> 
<asp:Parameter Name="City" Type="String" /> 
<asp:Parameter Name="Country" Type="String" /> 
<asp:Parameter Name="Phone" Type="String" /> 
</InsertParameters> 
<UpdateParameters> 
<asp:Parameter Name="FirstName" Type="String" /> 
<asp:Parameter Name="LastName" Type="String" /> 
<asp:Parameter Name="City" Type="String" /> 
<asp:Parameter Name="Country" Type="String" /> 
<asp:Parameter Name="Phone" Type="String" /> 
<asp:Parameter Name="original_Id" Type="Int32" /> 
<asp:Parameter Name="original_FirstName" Type="String" /> 
<asp:Parameter Name="original_LastName" Type="String" /> 
<asp:Parameter Name="original_City" Type="String" /> 
<asp:Parameter Name="original_Country" Type="String" /> 
<asp:Parameter Name="original_Phone" Type="String" /> 
</UpdateParameters> 
</asp:SqlDataSource> 
</form> 
</body> 
</html>


```

### 🅒  Create a web application to display Using Disconnected Data Access and Databinding using GridView.


**Gridview with Databinding:**

**Default.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" 
Inherits="_Default" %> 
<!DOCTYPE html> 
<html xmlns="http://www.w3.org/1999/xhtml"> 
<head runat="server"> 
<title></title> 
</head> 
<body> 
<form id="form1" runat="server"> 
<div> 
<asp:Button ID="Button1" runat="server" OnClick="Button1_Click" Text="Show 
Disconnected Data" /> 
</div> 
<br /> 
<asp:GridView ID="GridView1" runat="server" AutoGenerateColumns="False" 
DataKeyNames="Id" DataSourceID="SqlDataSource1"> 
<Columns> 
<asp:BoundField DataField="Id" HeaderText="Id" ReadOnly="True" SortExpression="Id" /> 
<asp:BoundField DataField="FirstName" HeaderText="FirstName" 
SortExpression="FirstName" />
<asp:BoundField DataField="LastName" HeaderText="LastName" 
SortExpression="LastName" /> 
<asp:BoundField DataField="City" HeaderText="City" SortExpression="City" /> 
<asp:BoundField DataField="Country" HeaderText="Country" SortExpression="Country" 
/> 
<asp:BoundField DataField="Phone" HeaderText="Phone" SortExpression="Phone" /> 
</Columns> 
</asp:GridView> 
<asp:SqlDataSource ID="SqlDataSource1" runat="server" 
ConflictDetection="CompareAllValues" ConnectionString="<%$ 
ConnectionStrings:ConnectionString %>" DeleteCommand="DELETE FROM [Student] WHERE 
[Id] = @original_Id AND (([FirstName] = @original_FirstName) OR ([FirstName] IS NULL AND 
@original_FirstName IS NULL)) AND (([LastName] = @original_LastName) OR ([LastName] IS 
NULL AND @original_LastName IS NULL)) AND (([City] = @original_City) OR ([City] IS 
NULL AND @original_City IS NULL)) AND (([Country] = @original_Country) OR ([Country] IS 
NULL AND @original_Country IS NULL)) AND (([Phone] = @original_Phone) OR ([Phone] IS 
NULL AND @original_Phone IS NULL))" InsertCommand="INSERT INTO [Student] ([Id], 
[FirstName], [LastName], [City], [Country], [Phone]) VALUES (@Id, @FirstName, @LastName, 
@City, @Country, @Phone)" OldValuesParameterFormatString="original_{0}" 
SelectCommand="SELECT * FROM [Student]" UpdateCommand="UPDATE [Student] SET 
[FirstName] = @FirstName, [LastName] = @LastName, [City] = @City, [Country] = @Country, 
[Phone] = @Phone WHERE [Id] = @original_Id AND (([FirstName] = @original_FirstName) OR 
([FirstName] IS NULL AND @original_FirstName IS NULL)) AND (([LastName] = 
@original_LastName) OR ([LastName] IS NULL AND @original_LastName IS NULL)) AND 
(([City] = @original_City) OR ([City] IS NULL AND @original_City IS NULL)) AND (([Country] 
= @original_Country) OR ([Country] IS NULL AND @original_Country IS NULL)) AND 
(([Phone] = @original_Phone) OR ([Phone] IS NULL AND @original_Phone IS NULL))"> 
<DeleteParameters> 
<asp:Parameter Name="original_Id" Type="Int32" /> 
<asp:Parameter Name="original_FirstName" Type="String" /> 
<asp:Parameter Name="original_LastName" Type="String" /> 
<asp:Parameter Name="original_City" Type="String" /> 
<asp:Parameter Name="original_Country" Type="String" /> 
<asp:Parameter Name="original_Phone" Type="String" /> 
</DeleteParameters> 
<InsertParameters> 
<asp:Parameter Name="Id" Type="Int32" /> 
<asp:Parameter Name="FirstName" Type="String" /> 
<asp:Parameter Name="LastName" Type="String" /> 
<asp:Parameter Name="City" Type="String" /> 
<asp:Parameter Name="Country" Type="String" /> 
<asp:Parameter Name="Phone" Type="String" /> 
</InsertParameters> 
<UpdateParameters> 
<asp:Parameter Name="FirstName" Type="String" /> 
<asp:Parameter Name="LastName" Type="String" /> 
<asp:Parameter Name="City" Type="String" /> 
<asp:Parameter Name="Country" Type="String" /> 
<asp:Parameter Name="Phone" Type="String" /> 
<asp:Parameter Name="original_Id" Type="Int32" /> 
<asp:Parameter Name="original_FirstName" Type="String" />
<asp:Parameter Name="original_LastName" Type="String" /> 
<asp:Parameter Name="original_City" Type="String" /> 
<asp:Parameter Name="original_Country" Type="String" /> 
<asp:Parameter Name="original_Phone" Type="String" /> 
</UpdateParameters> 
</asp:SqlDataSource> 
</form> 
</body> 
</html>

```

**Default.aspx.cs:**
```
using System; 
using System.Collections.Generic; 
using System.Linq; using 
System.Web; using System.Web.UI; 
using System.Web.UI.WebControls; 
using System.Data; using 
System.Data.SqlClient; using 
System.Configuration; 
 
public partial class _Default : System.Web.UI.Page 
{ 
protected void Page_Load(object sender, EventArgs e) 
{ 
 
} 
protected void Button1_Click(object sender, EventArgs e) 
{ 
string connStr = ConfigurationManager.ConnectionStrings["connStr"].ConnectionString; 
SqlConnection con=new SqlConnection(connStr); 
SqlDataAdapter objDa=new SqlDataAdapter(); 
DataSet objDs= new DataSet(); 
using (SqlConnection objConn = new SqlConnection(connStr)) 
{ 
SqlCommand objCmd = new SqlCommand("Select * from Student", objConn); 
objCmd.CommandType = CommandType.Text; 
objDa.SelectCommand = objCmd; 
objDa.Fill(objDs, "Product"); 
GridView1.DataSource = objDs.Tables[0]; 
GridView1.DataBind(); 
} 
} 
}



```

**Web.config::**
```

<?xml version="1.0"?>
<configuration>
<connectionStrings> 
<add name="ConnectionString" connectionString="Data 
Source=(LocalDB)\v11.0;AttachDbFilename=|DataDirectory|\Database.mdf;Integrated 
Security=True" 
providerName="System.Data.SqlClient" /> 
</connectionStrings> 
<system.web> 
<compilation debug="true" targetFramework="4.8.1" /> 
<httpRuntime targetFramework="4.8.1" /> 
</system.web> 
 
</configuration>


```


### 🅒  Create a web application for inserting and deleting records from a database. (Using Execute-Non Query). 


**Database:**

**WebForm1.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" 
Inherits="Pract7a.WebForm1" %> 
<!DOCTYPE html> 
<html xmlns="http://www.w3.org/1999/xhtml"> 
<head runat="server"> 
<title></title>
</head> 
<body> 
<form id="form1" runat="server"> 
<div> 
Enter Student 
Id:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 
<asp:TextBox ID="TextBox6" runat="server"></asp:TextBox> 
<br /> 
Enter Student FirstName:&nbsp; <asp:TextBox ID="TextBox1" 
runat="server"></asp:TextBox> 
<br /> 
Enter Student LastName:&nbsp; <asp:TextBox ID="TextBox2" runat="server"></asp:TextBox> 
<br /> 
Enter Student City:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 
<asp:TextBox ID="TextBox3" runat="server"></asp:TextBox> 
<br /> 
Enter Student Country:&nbsp;&nbsp;&nbsp;&nbsp; 
<asp:TextBox ID="TextBox4" runat="server"></asp:TextBox> 
<br /> 
Enter Student Phone:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 
<asp:TextBox ID="TextBox5" runat="server"></asp:TextBox> 
<br /> 
<br /> 
<asp:Button ID="Button1" runat="server" OnClick="Button1_Click" Text="Insert Record" /> 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbs 
p;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&n 
bsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 
&nbsp; 
<asp:Button ID="Button2" runat="server" OnClick="Button2_Click" Text="Delete Record" /> 
<br /> 
<br /> 
<asp:Label ID="Label1" runat="server" Text="Result:"></asp:Label> 
 
</div> 
</form> 
</body> 
</html>

```

**WebForm1.aspx.cs:**
```
using System; 
using System.Collections.Generic; 
using System.Linq; using 
System.Web; using System.Web.UI; 
using System.Web.UI.WebControls; 
using System.Data; using 
System.Data.SqlClient; 
using System.Configuration; 
 
namespace Pract7a 
{
public partial class WebForm1 : System.Web.UI.Page 
{ 
protected void Page_Load(object sender, EventArgs e) 
{ 
 
} 
 
protected void Button1_Click(object sender, EventArgs e) 
{ 
String connstr=ConfigurationManager.ConnectionStrings["connstr"].ConnectionString; 
SqlConnection con=new SqlConnection(connstr); 
string insertquery="insert into Student values(@Id, @FirstName, @LastName, @City, @Country, 
@Phone)"; 
SqlCommand cmd=new SqlCommand(insertquery,con); 
cmd.Parameters.AddWithValue("@FirstName",TextBox1.Text); 
cmd.Parameters.AddWithValue("@LastName",TextBox2.Text); 
cmd.Parameters.AddWithValue("@City",TextBox3.Text); 
cmd.Parameters.AddWithValue("@Country",TextBox4.Text); 
cmd.Parameters.AddWithValue("@Phone",TextBox5.Text); 
cmd.Parameters.AddWithValue("@Id", TextBox6.Text); con.Open(); 
cmd.ExecuteNonQuery(); 
Label1.Text="Record Inserted Successfully...!"; con.Close(); 
} 
 
protected void Button2_Click(object sender, EventArgs e) 
{ 
string connstr = ConfigurationManager.ConnectionStrings["connstr"].ConnectionString; 
SqlConnection con = new SqlConnection(connstr); string deletequery = "delete from 
person where Id=@Id"; SqlCommand cmd = new SqlCommand(deletequery, con); 
cmd.Parameters.AddWithValue("@Id", TextBox6.Text);  con.Open(); 
cmd.ExecuteNonQuery(); 
Label1.Text = "Record Deleted Successfully...!"; con.Close(); 
} 
} 
}


```

### 🅒  8.A) Create a web application to demonstrate use of GridView button column and GridView events along with paging and sorting. 


**Gridview:**

**Default.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" 
Inherits="_Default" %>
<!DOCTYPE html> 
<html xmlns="http://www.w3.org/1999/xhtml"> 
<head runat="server"> 
<title></title> 
</head> 
<body> 
<form id="form1" runat="server"> 
<div> 
<asp:GridView ID="GridView1" runat="server" AllowPaging="True" AllowSorting="True" 
AutoGenerateColumns="False" DataKeyNames="Id" DataSourceID="SqlDataSource1"> 
<Columns> 
<asp:BoundField DataField="Id" HeaderText="Id" ReadOnly="True" SortExpression="Id" 
/> 
<asp:BoundField DataField="First Name" HeaderText="First Name" 
SortExpression="First Name" /> 
<asp:BoundField DataField="Last Name" HeaderText="Last Name" SortExpression="Last 
Name" /> 
 <asp:BoundField DataField="City" HeaderText="City" SortExpression="City" /> 
<asp:BoundField DataField="Country" HeaderText="Country" SortExpression="Country" 
 /> 
 <asp:BoundField DataField="Phone " HeaderText="Phone " SortExpression="Phone " /> 
<asp:CommandField ButtonType="Button" HeaderText="EDIT" ShowEditButton="True" 
ShowHeader="True" /> 
<asp:CommandField ButtonType="Button" HeaderText="DELETE" 
ShowDeleteButton="True" ShowHeader="True" /> 
</Columns> 
</asp:GridView> 
<asp:SqlDataSource ID="SqlDataSource1" runat="server" 
ConflictDetection="CompareAllValues" ConnectionString="<%$ 
ConnectionStrings:ConnectionString %>" DeleteCommand="DELETE FROM [Student] WHERE 
[Id] = @original_Id AND (([First Name] = @original_First_Name) OR ([First Name] IS NULL 
AND @original_First_Name IS NULL)) AND (([Last Name] = @original_Last_Name) OR ([Last 
Name] IS NULL AND @original_Last_Name IS NULL)) AND (([City] = @original_City) OR
([City] IS NULL AND @original_City IS NULL)) AND (([Country] = @original_Country) OR 
([Country] IS NULL AND @original_Country IS NULL)) AND (([Phone ] = @original_Phone_) 
OR ([Phone ] IS NULL AND @original_Phone_ IS NULL))" InsertCommand="INSERT INTO 
[Student] ([Id], [First Name], [Last Name], [City], [Country], [Phone ]) VALUES (@Id, 
@First_Name, @Last_Name, @City, @Country, @Phone_)" 
OldValuesParameterFormatString="original_{0}" SelectCommand="SELECT * FROM [Student]" 
UpdateCommand="UPDATE [Student] SET [First Name] = @First_Name, [Last Name] = 
@Last_Name, [City] = @City, [Country] = @Country, [Phone ] = @Phone_ WHERE [Id] = 
@original_Id AND (([First Name] = @original_First_Name) OR ([First Name] IS NULL AND 
@original_First_Name IS NULL)) AND (([Last Name] = @original_Last_Name) OR ([Last Name] 
IS NULL AND @original_Last_Name IS NULL)) AND (([City] = @original_City) OR ([City] IS 
NULL AND @original_City IS NULL)) AND (([Country] = @original_Country) OR ([Country] IS 
NULL AND @original_Country IS NULL)) AND (([Phone ] = @original_Phone_) OR ([Phone ] IS 
NULL AND @original_Phone_ IS NULL))"> 
<DeleteParameters> 
<asp:Parameter Name="original_Id" Type="Int32" /> 
<asp:Parameter Name="original_First_Name" Type="String" /> 
<asp:Parameter Name="original_Last_Name" Type="String" /> 
<asp:Parameter Name="original_City" Type="String" /> 
<asp:Parameter Name="original_Country" Type="String" /> 
<asp:Parameter Name="original_Phone_" Type="String" /> 
</DeleteParameters> 
<InsertParameters> 
<asp:Parameter Name="Id" Type="Int32" /> 
<asp:Parameter Name="First_Name" Type="String" /> 
<asp:Parameter Name="Last_Name" Type="String" /> 
<asp:Parameter Name="City" Type="String" /> 
<asp:Parameter Name="Country" Type="String" /> 
<asp:Parameter Name="Phone_" Type="String" /> 
</InsertParameters> 
<UpdateParameters> 
<asp:Parameter Name="First_Name" Type="String" /> 
<asp:Parameter Name="Last_Name" Type="String" />
<asp:Parameter Name="City" Type="String" /> 
<asp:Parameter Name="Country" Type="String" /> 
<asp:Parameter Name="Phone_" Type="String" /> 
<asp:Parameter Name="original_Id" Type="Int32" /> 
<asp:Parameter Name="original_First_Name" Type="String" /> 
<asp:Parameter Name="original_Last_Name" Type="String" /> 
<asp:Parameter Name="original_City" Type="String" /> 
<asp:Parameter Name="original_Country" Type="String" /> 
<asp:Parameter Name="original_Phone_" Type="String" /> 
</UpdateParameters> 
</asp:SqlDataSource> 
</div> 
</form> 
</body> 
</html> 
```


### 🅒  8.A) EXCEPTION HANDELING. 


**Exception Handeling:**

**Default.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Exception Handling Example</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            Enter a number to divide 100 by: 
            <asp:TextBox ID="txtNumber" runat="server"></asp:TextBox>
            <asp:Button ID="btnDivide" runat="server" Text="Divide" OnClick="btnDivide_Click" />
            <br /><br />
            <asp:Label ID="lblResult" runat="server" ForeColor="Red"></asp:Label>
        </div>
    </form>
</body>
</html>

```

**Default.aspx.cs:**
```
using System;

public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {

    }

    protected void btnDivide_Click(object sender, EventArgs e)
    {
        try
        {
            // Convert input to integer
            int number = int.Parse(txtNumber.Text);

            // Perform division
            int result = 100 / number;

            // Display result
            lblResult.ForeColor = System.Drawing.Color.Green;
            lblResult.Text = "Result: " + result.ToString();
        }
        catch (DivideByZeroException ex)
        {
            lblResult.ForeColor = System.Drawing.Color.Red;
            lblResult.Text = "Error: Cannot divide by zero!";
        }
        catch (FormatException ex)
        {
            lblResult.ForeColor = System.Drawing.Color.Red;
            lblResult.Text = "Error: Please enter a valid number!";
        }
        catch (Exception ex)
        {
            lblResult.ForeColor = System.Drawing.Color.Red;
            lblResult.Text = "An unexpected error occurred: " + ex.Message;
        }
    }
}


```





