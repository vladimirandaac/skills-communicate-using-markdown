# Lorem ipsum dolor sit amet
## consectetur adipiscing elit
### ed do eiusmod tempor incididunt ut labore et dolore magna aliqua
#### Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
##### Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur
###### Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
![Image of Yaktocat](https://octodex.github.com/images/yaktocat.png)
```C#
  public string GeneraCodigoBarras(string codigoRepuesto)
        {
            string path = string.Format(@"{0}\BarCode\Repuestos", ConfigurationManager.AppSettings["imagenes"]);
            string path_completo = string.Format(@"{0}\BarCode\Repuestos\{1}.jpg", ConfigurationManager.AppSettings["imagenes"], codigoRepuesto);
            string url = string.Format("{0}BarCode/Repuestos/{1}.jpg", ConfigurationManager.AppSettings["url_imagenes"], codigoRepuesto);
            
            Barcode128 codigobarra = new Barcode128();
            codigobarra.CodeType = Barcode.CODE128;
            codigobarra.BarHeight = 50f;
            codigobarra.Code = codigoRepuesto;
            codigobarra.StartStopText = false;
            codigobarra.AltText = codigoRepuesto;
            codigobarra.Extended = true;
            codigobarra.Font = BaseFont.CreateFont(BaseFont.HELVETICA, BaseFont.CP1252, false);
            codigobarra.TextAlignment = Element.ALIGN_CENTER;
            System.Drawing.Image img = codigobarra.CreateDrawingImage(System.Drawing.Color.Black, System.Drawing.Color.White);

            if (File.Exists(path_completo))
                return url;

            if (!Directory.Exists(path))
            {
                Directory.CreateDirectory(path);
            }
            img.Save(path_completo, System.Drawing.Imaging.ImageFormat.Jpeg);

            return url;
        }
```
