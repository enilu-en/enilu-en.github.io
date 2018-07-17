---
layout:     post
title:      merge pdf online is coming
subtitle:   the most simple, using the best merge pdf online site is coming
date:       2018-07-17
author:     enilu
header-img: img/tag-bg-o.jpg
catalog: true
tags:
    - pdf
---

 

the most simple, using the best merge pdf online site is coming : 
[http://pdfmerge.online](http://pdfmerge.online)


Online PDF Merge is coming, The origin of this site is to start a network course, each class has a PDF courseware. I want to merge into a PDF file, so it looks convenient.

On the internet to find some online merge PDF tools, but not particularly useful, had to do one: Click here to try Http://pdfmerge.online/ Just started using Python to do a tool, the Internet has a lot of examples of Python merged pdf, I organized a bit, this can run through

```python
# -*- coding:utf-8*-
import sys
reload(sys)
sys.setdefaultencoding('utf-8')

import fnmatch
import os
import os.path
from pyPdf import PdfFileReader,PdfFileWriter
import time
time1=time.time()

def getFileName(filepath):
    file_list = []
    for n in range(1,10):
        file_list.append(str(n)+'.pdf')

    return file_list

def MergePDF(filepath,outfile):
    output=PdfFileWriter()
    outputPages=0
    pdf_fileName=getFileName(filepath)
    print pdf_fileName
    for each in pdf_fileName:
        
        input = PdfFileReader(file('/root/test/pdf/'+each, "rb"))

        
        if input.isEncrypted == True:
            input.decrypt("map")

        # get total pages of pdf
        pageCount = input.getNumPages()
        outputPages += pageCount
        print pageCount

        
        for iPage in range(0, pageCount):
            output.addPage(input.getPage(iPage))


    print "All Pages Number:"+str(outputPages)
    
    outputStream=file(filepath+outfile,"wb")
    output.write(outputStream)
    outputStream.close()
    print "finished"



if __name__ == '__main__':
    file_dir = r'/root/test/pdf/'
    out=u"out.pdf"
    MergePDF(file_dir,out)
    time2 = time.time()
    print u'use time：' + str(time2 - time1) + 's'

```

But what I want is an online PDF merge tool, so I built one with spring boot, and now that I'm using Java, I don't need to do a pdf merge with Python. Open source software Itext has a rich support for PDF operations, naturally incorporating merged PDFs, and the following is the core code for merging PDFs

```java
public class PdfService {
    public static void main(String[] args) {
        Map<Integer,String> files = new HashMap();
        files.put(0,"e:\\1.pdf");
        files.put(1, "e:\\2.pdf");
        files.put(2, "e:\\3.pdf" );
        String savepath = "e:\\temp.pdf";

        new PdfService().mergePdfFiles(files, savepath);
    }

    public  boolean mergePdfFiles(Map<Integer,String> files, String newfile) {
        boolean retValue = false;
        Document document = null;
        try {
            document = new Document(new PdfReader(files.get(0)).getPageSize(1));
            PdfCopy copy = new PdfCopy(document, new FileOutputStream(newfile));
            document.open();
            for (int i = 0; i < files.size(); i++) {
                PdfReader reader = new PdfReader(files.get(i));
                int n = reader.getNumberOfPages();
                for (int j = 1; j <= n; j++) {
                    document.newPage();
                    PdfImportedPage page = copy.getImportedPage(reader, j);
                    copy.addPage(page);
                }
            }
            retValue = true;
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            document.close();
        }
        return retValue;
    }
}

```

## Useage 
![](https://raw.githubusercontent.com/enilu-en/enilu-en.github.io/master/img/2018/home.jpg)

![](https://raw.githubusercontent.com/enilu-en/enilu-en.github.io/master/img/2018/upload.png)

![](https://raw.githubusercontent.com/enilu-en/enilu-en.github.io/master/img/2018/merge.jpg)
 