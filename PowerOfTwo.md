Shows code to resize a TPHXImage into power of two size

# Introduction #

Many graphic card doesnt support non power of two textures, this might be a problem when using background textures in your games.

Here is a small snippet that loads and converts an image into a power of two size in runtime.


# Details #

```

uses phxGraphics;

//------------------------------------------------------------------------------
procedure LoadAndResize(const FileName: String; const Image: TPHXImage);
var Bitmap: TPHXBitmap;
begin
  Bitmap:= TPHXBitmap.Create;
  try
    Bitmap.LoadBitmap(FileName);

    Image.Patterns.Add('', 0, 0, Bitmap.Width, Bitmap.Height);

    Bitmap.ResizeCanvasPowerOfTwo();

    Image.Texture.Import(Bitmap.Graphic);
    Image.Texture.Build;

    Image.Width:= Bitmap.Width;
    Image.Height:= Bitmap.Height;
    Image.Initialize;

  finally
    Bitmap.Free;
  end;
end;

```