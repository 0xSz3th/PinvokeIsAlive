
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool IsCharLower(char ch);
```

## C# Signature:
```cs
public partial class Form1 : Form
    {
    public Form1()
    {
        InitializeComponent();
    }
```

## C# Signature:
```cs
[DllImport("user32.dll")]
    static extern bool IsCharLower(char ch);

    private void button1_Click(object sender, EventArgs e)
    {

        try
        {

        char ch = Convert.ToChar(textBox1.Text);
```

## C# Signature:
```cs
if (IsCharLower(ch))
        {
            label1.Text = " Lowercase characters are entered and Compiler 1 is returned.";
            label2.Text = " Character Entered Is =   " + ch.ToString();
        }
        else
        {

            label1.Text = "Entered in uppercase characters or numbers or symbols and compiler 0 is returned.";
            label2.Text = " Character Entered Is =   " + ch.ToString();
        }
```

## C# Signature:
```cs
textBox1.Clear();

        }
```

## C# Signature:
```cs
catch
        {
        MessageBox.Show(
        "Please enter a character.",
        " ", MessageBoxButtons.OK, MessageBoxIcon.Error);
        }
      }
    }
      }
```
