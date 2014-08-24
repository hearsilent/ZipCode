ZipCode
=======
如需使用本模組完整功能需下載 :    
1. [ZipCode 3+2 XML][1] (官方網頁)  
2. [ZipCode 3+2 XML][4] (DropBox備份)      
3. [Json.Net][2]   
                            
本模組需使用Zip.txt (請放置在與程式同目錄下) :     
1. [Zip.txt][3] (以官方2014/7 XML製作)    
                    
備註 :     
使用本模組建議以Thread方式 , 避免UI Crash.           
```   
Imports System.Threading
Dim ZipCodeThread As Thread
Private Sub Address_TextChanged(sender As Object, e As EventArgs) Handles Address.TextChanged
    ZipCodeThread = New Thread(AddressOf Me.ZipCodeBackground)
    ZipCodeThread.Start()
End Sub 
```
```
Sub ZipCodeBackground()
    Dim newAddress As New SilentAddressClass(Address.Text)

    If (Not newAddress.City = "" Or Not newAddress.Town = "") And newAddress.Road = "" Then
        ZipCode.Text = newAddress.Zip
    End If
    If Not newAddress.No = "" And Address.Text.Contains("號") Then
        ZipCode.Text = newAddress.Zip
        'ZipCodeThread = New Thread(AddressOf ZipCodeBackground)
        'ZipCodeThread.Start()
    End If

    If CityComboBox.Items.Contains(newAddress.City) Then
        For i = 0 To CityComboBox.Items.Count - 1
            If CityComboBox.Items.Item(i) = newAddress.City Then
                CityComboBox.SelectedIndex = i
                GoTo District
            End If
        Next
        Exit Sub
District:
        If DistrictComboBox.Items.Contains(newAddress.Town) Then
            For i = 0 To DistrictComboBox.Items.Count - 1
                If DistrictComboBox.Items.Item(i) = newAddress.Town Then
                    DistrictComboBox.SelectedIndex = i
                    Exit For
                End If
            Next
        End If
    End If
End Sub
```    

[1]: http://www.post.gov.tw/post/internet/Download/all_list.jsp?ID=2201#dl_txt_s_A0206
[2]: https://json.codeplex.com/releases
[3]: https://www.dropbox.com/s/30lfni4jpdkoy28/Zip.txt?dl=0
[4]: https://www.dropbox.com/s/qrk2yfo6zc941tl/Zip32_10307.xml?dl=0