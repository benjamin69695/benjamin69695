<Window x:Name="hotkeyWindow" x:Class="AlphaClicker.ChangeHotkey"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:AlphaClicker"
        mc:Ignorable="d"
        ResizeMode="CanMinimize"
        WindowStyle="None"
        Title="Alpha Clicker"
        Height="155" Width="300"
        Background="{x:Null}"
        AllowsTransparency="True" MouseLeftButtonDown="hotkeyWindow_MouseLeftButtonDown" PreviewKeyDown="hotkeyWindow_PreviewKeyDown" Loaded="hotkeyWindow_Loaded" Closing="hotkeyWindow_Closing">
        AllowsTransparency="True"
        MouseLeftButtonDown="hotkeyWindow_MouseLeftButtonDown" PreviewKeyDown="hotkeyWindow_PreviewKeyDown" MouseDown="hotkeyWindow_MouseDown" Loaded="hotkeyWindow_Loaded" Closing="hotkeyWindow_Closing">

    <Window.Triggers>
        <EventTrigger RoutedEvent="Window.Loaded">
  42 changes: 42 additions & 0 deletions42  
Alphaclicker/ChangeHotkey.xaml.cs
Original file line number	Diff line number	Diff line change
@@ -88,6 +88,20 @@ private string CodeToSpecialKey(int key)
            return "";
        }

        private string CodeToSpecialMouseButton(int key)
        {
            switch (key)
            {
                case 4:
                    return "MMB";
                case 5:
                    return "X1";
                case 6:
                    return "X2";
            }
            return "";
        }

        private bool hasSpecKey = false;
        private int key1 = -1;
        private int key2 = -1;
@@ -141,6 +155,34 @@ private void hotkeyWindow_PreviewKeyDown(object sender, KeyEventArgs e)
            }
        }

        private void hotkeyWindow_MouseDown(object sender, MouseButtonEventArgs e)
        {
            if (!startBtn.IsEnabled)
            {
                for (int i = 4; i < 7; i++)
                {
                    if (WinApi.GetAsyncKeyState(i) > 0)
                    {
                        /* If middle or special mouse button */
                        if (i >= 4 && i <= 6)
                        {
                            if (keyBox.Text == "Press Keys")
                            {
                                keyBox.Clear();
                            }

                            keyBox.AppendText(CodeToSpecialMouseButton(i));
                            startBtn.IsEnabled = true;
                            key2 = i;
                            okBtn.IsEnabled = true;
                            break;
                        }
                    }

                }
            }
        }

        private void startBtn_Click(object sender, RoutedEventArgs e)
        {
            okBtn.IsEnabled = false;
