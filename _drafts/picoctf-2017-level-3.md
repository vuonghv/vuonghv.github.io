---
layout: post
title:  "Write up PicoCTF 2017 level 3"
categories: ctf
---

## [Reverse engineering - 115] Coffee
> You found a suspicious USB drive in a jar of pickles. It contains this [file](https://webshell2017.picoctf.com/static/90046e7cd0d4e2f6153ac81b978b66ee/freeThePickles.class) file.

The file is a Java class file, containing Java bytecodes.
Let's decompile it, I use [Decompilers online](http://www.javadecompilers.com), and have the source code. Too easy, huh.

```java
import java.util.Base64.Decoder;

public class problem {
  public problem() {}

  public static String get_flag() { String str1 = "Hint: Don't worry about the schematics";
    String str2 = "eux_Z]\\ayiqlog`s^hvnmwr[cpftbkjd";
    String str3 = "Zf91XhR7fa=ZVH2H=QlbvdHJx5omN2xc";
    byte[] arrayOfByte1 = str2.getBytes();
    byte[] arrayOfByte2 = str3.getBytes();
    byte[] arrayOfByte3 = new byte[arrayOfByte2.length];
    for (int i = 0; i < arrayOfByte2.length; i++)
    {
      arrayOfByte3[i] = arrayOfByte2[(arrayOfByte1[i] - 90)];
    }
    System.out.println(java.util.Arrays.toString(java.util.Base64.getDecoder().decode(arrayOfByte3)));
    return new String(java.util.Base64.getDecoder().decode(arrayOfByte3));
  }

  public static void main(String[] paramArrayOfString) {
    System.out.println("Nothing to see here");
  }
}
```

Flag: `flag_{pretty_cool_huh}`
