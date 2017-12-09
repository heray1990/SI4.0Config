# SI4.0Config

Configuration for Source Insight 4.0

## Set a macro

[utils.em](https://github.com/heray1990/SI4.0Config/blob/master/Users/Documents/Source%20Insight%204.0/Base/utils.em) is a base macro file for projects. We can add some macro and register a hotkey for it.

For example, let's add a macro `CodeBlockComment` for setting a block of code as comment automatically. Instructions for use:

**Project** -> **Open Project...**, then open base project *Users\Documents\Source Insight 4.0\Projects\Base\Base*.

Open *utils.em* file and add the following code at the end of it.

```
// Set a block of code as comment.
// Add "#if 0" in front of a block of code and add "#endif" after.
macro CodeBlockComment()  
{  
    hwnd=GetCurrentWnd()  
    sel=GetWndSel(hwnd)  
    lnFirst=GetWndSelLnFirst(hwnd)  
    lnLast=GetWndSelLnLast(hwnd)  
    hbuf=GetCurrentBuf()  
   
    if(LnFirst == 0) {  
            szIfStart = ""  
    }else{  
            szIfStart = GetBufLine(hbuf, LnFirst-1)  
    }  
    szIfEnd = GetBufLine(hbuf, lnLast+1)  
    if(szIfStart == "#if 0" && szIfEnd == "#endif") {  
            DelBufLine(hbuf, lnLast+1)  
            DelBufLine(hbuf, lnFirst-1)  
            sel.lnFirst = sel.lnFirst – 1  
            sel.lnLast = sel.lnLast – 1  
    }else{  
            InsBufLine(hbuf, lnFirst, "#if 0")  
            InsBufLine(hbuf, lnLast+2, "#endif")  
            sel.lnFirst = sel.lnFirst + 1  
            sel.lnLast = sel.lnLast + 1  
    }  
   
    SetWndSel( hwnd, sel )  
}
```

Now we added a macro, then we set a hotkey for it.

**Options** -> **Key Assignments...**, input `CodeBlockComment` in **Command**, then select **Assign New Key...** and enter your hotkey, for example, *Ctrl + #*. At last, select **OK**.

Now if you open another project, just press *Ctrl + #* and a block of code you selected will be set as comment.

## Configuration

Files in *Users\Documents\Source Insight 4.0\Settings* are configuration files for Source Insight 4.0.