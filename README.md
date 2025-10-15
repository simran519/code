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


**5. CustomValidator:**

**WebForm1.aspx:**
```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="WebForm1.aspx.cs" 
Inherits="_Default" %> 
<!DOCTYPE html> 
<html xmlns="http://www.w3.org/1999/xhtml"> 
<head id="Head1" runat="server"> 
<title></title> 
</head> 
<body> 
<form id="form1" runat="server"> 
<div> 
<asp:Label ID="Label1" runat="server" Text="Enter Number: "></asp:Label> 
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox> 
<asp:CustomValidator ID="CustomValidator1" runat="server" ControlToValidate="TextBox1" 
ErrorMessage="Enter number which is divisible by 2" ForeColor="Red" 
OnServerValidate="CustomValidator1_ServerValidate"></asp:CustomValidator> 
</div> 
<p> 
<asp:Button ID="Button1" runat="server" Text="Submit" OnClick="Button1_Click" /> 
</p><p> 
<asp:Label ID="Label2" runat="server" Text="Result:"></asp:Label> 
</p> 
</form>
</body> 
</html> 

```

**WebForm1.aspx.cs:**
```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
public partial class
    _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs
        e)
    {
    }
    protected void Button1_Click(object sender, EventArgs e)
    {
        Label2.Text += TextBox1.Text;
    }
    protected void CustomValidator1_ServerValidate(object source, ServerValidateEventArgs args)
    {
        int num = int.Parse(TextBox1.Text);
        if (num % 2 == 0)
        {
            args.IsValid
                = true;

        }
        else
        {
            args.IsValid = false;
        }
    }
}



```

**Web.config:**
```
<?xml version="1.0"?>
<configuration>
  <appSettings>
    <add key="ValidationSettings:UnobtrusiveValidationMode" value="None"/>
  </appSettings>
  <system.web>
    <compilation debug="true" targetFramework="4.5" />
    <httpRuntimetargetFramework="4.5" />
  </system.web>
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

**1.  User Control:**

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







