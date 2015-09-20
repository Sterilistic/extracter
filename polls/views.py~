from django.shortcuts import render
from django.http import HttpResponse
import csv
from django.utils.encoding import smart_str
import mimetypes
import urllib
import lxml.html
from django.core.servers.basehttp import FileWrapper

def home(request):
    if request.method == 'POST':
        para=request.POST['webpage']
        connection = urllib.urlopen(para)
	words=[]
        dom =  lxml.html.fromstring(connection.read())

        #for link in dom.xpath('//a/@href'): # select the url in href for all a tags(links)
             #words.append(link)

        with open("output.csv", 'wb') as f:
            writer = csv.writer(f)
            for link in dom.xpath('//a/@href'):    
                writer.writerow([['URLs'],[link]])
        filename = "output.csv"
        wrapper = FileWrapper(open(filename))
        content_type = mimetypes.guess_type(filename)[0]
        response = HttpResponse(wrapper,content_type=content_type)
        response['Content-Disposition'] = "attachment; filename=%s"%"output.csv"
        return response
    return render(request, "somepage.html")
