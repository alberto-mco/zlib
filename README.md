# ZLib
.Net ZLib implementation

My ZLib implementation has 3 classes:

- ZLibStream.cs
- ZLibHeader.cs
- Adler32.cs

<b>ZlibStream</b></br>
This class contains the I/O functions to correctly read or write the ZLib stream. Also, it has the control to determine if it's a supported ZLib stream or not.

<b>ZLibHeader</b></br>
The ZlibHeader class has the functions for encode or decode the ZLib header.

<b>Adler32</b></br>
This class has the functions for check the hash in Adler32. The result determines if the stream is correct or not.

## How to compress using the library
```C#
Using System.IO.Compression;
Using ZLib;

.
.
.

OpenFileDialog dlgOpen = new OpenFileDialog();
CompressionLevel level = CompressionLevel.Optimal;

if (dlgOpen.ShowDialog() == DialogResult.OK)
{
    using (FileStream fsSource = new FileStream(dlgOpen.FileName, FileMode.Open, FileAccess.Read))
    {
        using (FileStream fsTarget = new FileStream(dlgOpen.FileName + ".zlib", FileMode.Create, FileAccess.Write))
        {
            using (ZLIBStream zs = new ZLIBStream(fsTarget, level, true))
            {
                int bytesLeidos = 0;
                byte[] buffer = new byte[1024];

                while ((bytesLeidos = fsSource.Read(buffer, 0, buffer.Length)) > 0) 
                {
                    zs.Write(buffer, 0,bytesLeidos);                        
                }
            }
        }
    }
}
```

## How to compress using the library
```C#
Using System.IO.Compression;
Using ZLib;

.
.
.

OpenFileDialog dlgOpen = new OpenFileDialog();

if (dlgOpen.ShowDialog() == DialogResult.OK)
{ 
    using (FileStream fsSource = new FileStream(dlgOpen.FileName, FileMode.Open, FileAccess.Read))
    {
        using (ZLIBStream zs = new ZLIBStream(fsSource, CompressionMode.Decompress, true))
        {
            using (FileStream fsTarget = new FileStream(dlgOpen.FileName + ".txt", FileMode.Create, FileAccess.Write))
            {
                int bytesLeidos = 0;
                byte[] buffer = new byte[1024];

                while ((bytesLeidos = zs.Read(buffer, 0, buffer.Length)) > 0)
                {
                    fsTarget.Write(buffer, 0, bytesLeidos);
                }
            }
        }
    }
}
```
