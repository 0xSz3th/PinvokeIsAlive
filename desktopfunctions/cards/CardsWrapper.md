# CardsWrapper

using System; using System.Drawing; using System.Runtime.InteropServices;

namespace Cards {     ///

&#x20;   /// Class wrapper to Cards.dll     ///    public sealed class Card     {         #region API Declares         \[DllImport("cards.dll")]         private static extern bool cdtInit(\[In] ref int width, \[In] ref int height);

&#x20;       \[DllImport("cards.dll")]         private static extern void cdtTerm();

&#x20;       \[DllImport("cards.dll")]         private static extern int cdtDrawExt(IntPtr hDC, int x, int y, int dx, int dy,             int ecsCard, int ectDraw, int clr);

&#x20;       \[DllImport("cards.dll")]         private static extern int cdtDraw(IntPtr hDC, int x, int y, int ecsCard,             int ectDraw, int clr);

&#x20;       \[DllImport("cards.dll")]         private static extern int cdtAnimate(IntPtr hDC, int ecbCardBack, int x, int y, int iState);         #endregion

&#x20;       \#region fields         private static int \_standardWidth;         private static int \_standardHeight;         #endregion

&#x20;       \#region Constructor         static Card()         {             bool ret = Card.cdtInit(ref \_standardWidth, ref \_standardHeight);             if (!ret)                 throw new ApplicationException("Can't load cards.dll !");

&#x20;           // free up library when process exits             AppDomain.CurrentDomain.ProcessExit += new EventHandler(CurrentDomain\_ProcessExit);         }         #endregion

&#x20;       \#region Public Static Members         public static void DrawFace(Graphics g, int x, int y, int width, int height, int faceValue, CardSuit suit, Color invertedColor)         {             if (faceValue<0 || faceValue>12)                 throw new ArgumentOutOfRangeException("FaceValue", faceValue, "faceValue must be in the range 0 - 12.");

&#x20;           int cardValue = (int)suit  + faceValue \* 4;             IntPtr hDc = g.GetHdc();             try             {                 cdtDrawExt(hDc, x, y, width, height, cardValue, invertedColor!=Color.Empty ? 2 : 0, ConvertColor(invertedColor));             }             finally             {                 g.ReleaseHdc(hDc);             }         }         public static void DrawFace(Graphics g, int x, int y, int width, int height, int faceValue, CardSuit suit)         {             DrawFace(g, x, y, width, height, faceValue, suit, Color.Empty);         }         public static void DrawFace(Graphics g, int x, int y, int faceValue, CardSuit suit, Color invertedColor)         {             if (faceValue<0 || faceValue>12)                 throw new ArgumentOutOfRangeException("FaceValue", faceValue, "faceValue must be in the range 0 - 12.");

&#x20;           int cardValue = (int)suit  + faceValue \* 4;             IntPtr hDc = g.GetHdc();             try             {                 cdtDraw(hDc, x, y, cardValue, invertedColor!=Color.Empty ? 2 : 0, ConvertColor(invertedColor));             }             finally             {                 g.ReleaseHdc(hDc);             }         }         public static void DrawFace(Graphics g, int x, int y, int faceValue, CardSuit suit)         {             Card.DrawFace(g, x, y, faceValue, suit, Color.Empty);         }         public static void DrawDeck(Graphics g, int x, int y, int width, int height, CardDeck deck)         {             IntPtr hDc = g.GetHdc();             try             {                 cdtDrawExt(hDc, x, y, width, height, (int)deck, 1, 0);             }             finally             {                 g.ReleaseHdc(hDc);             }         }         public static void DrawDeck(Graphics g, int x, int y, CardDeck deck)         {             IntPtr hDc = g.GetHdc();             try             {                 cdtDraw(hDc, x, y, (int)deck, 1, 0);             }             finally             {                 g.ReleaseHdc(hDc);             }         }         public static void DrawDeck(Graphics g, int x, int y, int width, int height, Color backgroundColor)         {             IntPtr hDc = g.GetHdc();             try             {                 cdtDrawExt(hDc, x, y, width, height, (int)CardDeck.CrossHatch, 1, Card.ConvertColor(backgroundColor));             }             finally             {                 g.ReleaseHdc(hDc);             }         }         public static void DrawDeck(Graphics g, int x, int y, Color backgroundColor)         {             IntPtr hDc = g.GetHdc();             try             {                 cdtDraw(hDc, x, y, (int)CardDeck.CrossHatch, 1, Card.ConvertColor(backgroundColor));             }             finally             {                 g.ReleaseHdc(hDc);             }         }         #endregion

&#x20;       \#region Properties         ///

&#x20;       /// Gets the standard width of the cards.         ///        public static int StandardWidth         {             get             {                 return Card.\_standardWidth;             }         }         ///        /// Gets the standard height of the cards.         ///        public static int StandardHeight         {             get             {                 return Card.\_standardHeight;             }         }         #endregion

&#x20;       \#region private members         private static void CurrentDomain\_ProcessExit(object sender, EventArgs e)         {             Card.cdtTerm();         }         private static int ConvertColor(Color c)         {             if (c!=Color.Empty)                 return (Convert.ToInt32(c.B) << 16) + (Convert.ToInt32(c.G) << 8) + c.R;             return 0;         }         #endregion     }

&#x20;   \#region enums     public enum CardSuit : int     {         Clubs = 0,         Diamonds = 1,         Hearts = 2,         Spades = 3     }     public enum CardDeck : int     {         CrossHatch = 53,         Weave1 = 54,         Weave2 = 55,         Robot = 56,         Flowers = 57,         Vine1 = 58,         Vine2 = 59,         Fish1 = 60,         Fish2 = 61,         Shells = 62,         Castle = 63,         Island = 64,         CardHand = 65,         The\_X = 67,         The\_O = 68     }     #endregion } Namespace Cards     '''

&#x20;   ''' Wrapper class for the Cards.dll     '''    Public NotInheritable Class Card

\#Region "API Deceleration"

&#x20;   Private Declare Function cdtInit Lib "cards.dll" (ByRef width As Integer, ByRef height As Integer) As Boolean

&#x20;   Private Declare Sub cdtTerm Lib "cards.dll" ()

&#x20;   Private Declare Function cdtDraw Lib "cards.dll" (ByVal hDC As IntPtr, ByVal x As Integer, ByVal y As Integer, ByVal ecsCard As Integer, ByVal ectDraw As Integer, ByVal clr As Integer) As Integer

&#x20;   Private Declare Function cdtDrawExt Lib "cards.dll" (ByVal hDC As IntPtr, ByVal x As Integer, ByVal y As Integer, ByVal dx As Integer, ByVal dy As Integer, ByVal ecsCard As Integer, ByVal ectDraw As Integer, ByVal clr As Integer) As Integer

&#x20;   Private Declare Function cdtAnimate Lib "cards.dll" (ByVal hDC As IntPtr, ByVal ecbCardBack As Integer, ByVal x As Integer, ByVal y As Integer, ByVal iState As Integer)

\#End Region

\#Region "Fields"

&#x20;   Private Shared \_standardWidth As Integer

&#x20;   Private Shared \_standardHeight As Integer

\#End Region

\#Region "Constructor"

&#x20;   Shared Sub New()         Dim ret As Boolean = Card.cdtInit(\_standardWidth, \_standardHeight)

&#x20;       If (Not ret) Then         Throw New ApplicationException("Can't load 'cards.dll'!")         End If

&#x20;       ' Free up library when process exits         AddHandler AppDomain.CurrentDomain.ProcessExit, AddressOf CurrentDomain\_ProcessExit     End Sub

\#End Region

\#Region "Public Shared Members"

&#x20;   Public Shared Sub DrawFace(ByVal g As Graphics, ByVal x As Integer, ByVal y As Integer, ByVal width As Integer, ByVal height As Integer, ByVal faceValue As Integer, ByVal suit As CardSuit, ByVal invertedColor As Color)         If (faceValue < 0 OrElse faceValue > 12) Then         Throw New ArgumentOutOfRangeException("FaceValue", faceValue, "faceValue must be in the range 0 - 12.")         End If

&#x20;       Dim cardValue As Integer = DirectCast(suit, Integer) + faceValue \* 4         Dim hDC As IntPtr = g.GetHdc()

&#x20;       Try         cdtDrawExt(hDC, x, y, width, height, cardValue, IIf(invertedColor <> Color.Empty, 2, 0), ConvertColor(invertedColor))         Finally         g.ReleaseHdc(hDC)         End Try     End Sub

&#x20;   Public Shared Sub DrawFace(ByVal g As Graphics, ByVal x As Integer, ByVal y As Integer, ByVal width As Integer, ByVal height As Integer, ByVal faceValue As Integer, ByVal suit As CardSuit)         DrawFace(g, x, y, width, height, faceValue, suit, Color.Empty)     End Sub

&#x20;   Public Shared Sub DrawFace(ByVal g As Graphics, ByVal x As Integer, ByVal y As Integer, ByVal faceValue As Integer, ByVal suit As CardSuit, ByVal invertedColor As Color)         If faceValue < 0 OrElse faceValue > 12 Then         Throw New ArgumentOutOfRangeException("FaceValue", faceValue, "faceValue must be in the range 0 - 12.")

&#x20;       Dim cardValue As Integer = DirectCast(suit, Integer) + faceValue \* 4         Dim hDc As IntPtr = g.GetHdc()

&#x20;       Try             cdtDraw(hDc, x, y, cardValue, IIf(invertedColor <> Color.Empty, 2, 0), ConvertColor(invertedColor))         Finally             g.ReleaseHdc(hDc)         End Try         End If     End Sub

&#x20;   Public Shared Sub DrawFace(ByVal g As Graphics, ByVal x As Integer, ByVal y As Integer, ByVal faceValue As Integer, ByVal suit As CardSuit)         Card.DrawFace(g, x, y, faceValue, suit, Color.Empty)     End Sub

&#x20;   Public Shared Sub DrawDeck(ByVal g As Graphics, ByVal x As Integer, ByVal y As Integer, ByVal width As Integer, ByVal height As Integer, ByVal deck As CardDeck)         Dim hDc As IntPtr = g.GetHdc()

&#x20;       Try         cdtDrawExt(hDc, x, y, width, height, DirectCast(deck, Integer), 1, 0)         Finally         g.ReleaseHdc(hDc)         End Try     End Sub

&#x20;   Public Shared Sub DrawDeck(ByVal g As Graphics, ByVal x As Integer, ByVal y As Integer, ByVal deck As CardDeck)         Dim hDc As IntPtr = g.GetHdc()

&#x20;       Try         cdtDraw(hDc, x, y, DirectCast(deck, Integer), 1, 0)         Finally         g.ReleaseHdc(hDc)         End Try     End Sub

&#x20;   Public Shared Sub DrawDeck(ByVal g As Graphics, ByVal x As Integer, ByVal y As Integer, ByVal width As Integer, ByVal height As Integer, ByVal backgroundColor As Color)         Dim hDc As IntPtr = g.GetHdc()

&#x20;       Try         cdtDrawExt(hDc, x, y, width, height, DirectCast(CardDeck.CrossHatch, Integer), 1, Card.ConvertColor(backgroundColor))         Finally         g.ReleaseHdc(hDc)         End Try     End Sub

&#x20;   Public Shared Sub DrawDeck(ByVal g As Graphics, ByVal x As Integer, ByVal y As Integer, ByVal backgroundColor As Color)         Dim hDc As IntPtr = g.GetHdc()

&#x20;       Try         cdtDraw(hDc, x, y, DirectCast(CardDeck.CrossHatch, Integer), 1, Card.ConvertColor(backgroundColor))         Finally         g.ReleaseHdc(hDc)         End Try     End Sub

\#End Region

\#Region "Properties"

&#x20;   Public Shared ReadOnly Property StandardWith() As Integer         Get         Return Card.\_standardWidth         End Get     End Property

&#x20;   Public Shared ReadOnly Property StandardHeight() As Integer         Get         Return Card.\_standardHeight         End Get     End Property

\#End Region

\#Region "private members"

&#x20;   Private Shared Sub CurrentDomain\_ProcessExit(ByVal sender As Object, ByVal e As EventArgs)         Card.cdtTerm()     End Sub

&#x20;   Private Shared Function ConvertColor(ByVal c As Color) As Integer         If c <> Color.Empty Then         Return (Convert.ToInt32(c.B) << 16) + (Convert.ToInt32(c.G) << 8) + c.R         End If         Return 0     End Function

\#End Region

\#Region "enums"

&#x20;   Public Enum CardSuit As Integer         Clubs = 0         Diamonds = 1         Hearts = 2         Spades = 3     End Enum

&#x20;   Public Enum CardDeck As Integer         CrossHatch = 53         Weave1 = 54         Weave2 = 55         Robot = 56         Flowers = 57         Vine1 = 58         Vine2 = 59         Fish1 = 60         Fish2 = 61         Shells = 62         Castle = 63         Island = 64         CardHand = 65         The\_X = 67         The\_O = 68     End Enum

\#End Region

&#x20;   End Class End Namespace
