 hugh
:
BitmapData.getData calls getPixels which copies the contents to a byte array.  If you modify the array, you will need to set it back the the image.   The code to directly access the pixels is a little out of date, but it can be used - and possibly updated using the same underlying calls.
[
04:16
]
hugh
:

   #if cpp
      var native = nme.native.ImageBuffer.fromBitmapData(bmp);
      if (native!=null)
      {
         var mutablePtr = native.value.Edit();
         for(i in 0...native.value.Width()*native.value.Height())
         {
            mutablePtr.setAt(i*3,0);
            mutablePtr.setAt(i*3+1,255);
            mutablePtr.setAt(i*3+2,0);
         }
      }
  #end

[
04:17
]
hugh
:
You will need to be careful with the pixel format - it may be stored ad RGB or RGBA or even something else if you are creating special images.
