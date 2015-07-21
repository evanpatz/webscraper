# webscraper

import urllib.request

'''
Steps for scraping a site:
1. Create a .txt file with the URLs of the website, either from the sitemap 
   provided in the site or by an online sitemap generator
   (one URL per line/ideally only product page URLs)
2. Run page_info() on one of the product pages.
3. From the page_info() output, find the beginning and ending strings for each
   category of the page_scraper and enter those in as the variables in page_scraper()
4. Run page_scraper() to see if the output is correct. Depending on the code of
   the site, you may need to add customized code to fix the output.
5. Once page_scraper() works correctly, run site_scraper() with the URLs file generated
   in the first step.
6. Be patient. Some websites have huge inventories and site_scraper() can take 
   multiple hours to scrape the entire site.
7. Once site_scraper() is finished running, upload the .txt file to an excel 
   spreadsheet or GoogleDocs.
'''

def page_info(web_page, file):
    '''
    Parameters: 
        web_page: enter the url of a product page to examine the code
        file: enter a blank .txt file to output the page code
    Use this function to determine the exact code of the product page. Use the 
    output code in the text file to find unique markers in the code to be used 
    in the scraper (below) for the name, price, brand, description, etc. 
    '''
    html = urllib.request.urlopen(web_page)
    for line in html: 
        line = line.decode('ascii', 'ignore')
        string_to_file(line, file)
    
def page_scraper(web_page):
    '''
    Parameters:
        web_page: enter the url of a product page from the website you're scraping
    This function scrapes info from a single web page. In the variables below, 
    enter unique strings that come directly before and after the target string 
    you are looking for. Once you examine the page's code generated 
    by page_info(), find a line of code where each charteristic of the product
    is listed. For example, if the name of a product is Patagonia Full-Zip Jacket,
    and the line of code is <span class="product-title">Patagonia Full-Zip Jacket</span>, 
    the beginning name variable, name_s, will be '<span class="product-title">'
    and the ending name variable, name_e, will be '</span>'. The scraper will return
    the target string that comes between these start and end strings. Important:
    the start, end, and target strings must all be on the SAME line of code. 
    Repeat for all variables; add or delete variables depending on what you want
    to scrape. 
    '''
    name_s = 
    name_e = 
    brand_s = 
    brand_e =
    sku_s = 
    sku_e = 
    cost_s = 
    cost_e = 
    des_s = 
    des_e =  
    size_s = 
    size_e = 
    color_s = 
    color_e =  
    cat_s = 
    cat_e = 

      
    info_list = [name_s, name_e, brand_s, brand_e, sku_s, sku_e, cost_s, 
                 cost_e, des_s, des_e, size_s, size_e, color_s, color_e, cat_s,
                 cat_e]

    #Enter the .txt file where the scraper will write the output
    file = 

    html = urllib.request.urlopen(web_page)

    for line in html: 
        line = line.decode('ascii', 'ignore')
        for i in range(len(info_list) - 1):
            if info_list[i] in line and i%2 == 0: 
                line_to_string(info_list[i], info_list[i+1], line, file)
    string_to_file("\n", file)

                    
def site_scraper(url_file, starting_url):
    '''
    Parameters:
        url_file: a .txt file with one URL per line
        starting_url: the line number of the URL that you want the program to 
                      start scraping from. When you begin, enter 0. However,
                      if the program stops due to a broken URL or a lost 
                      connection, enter the last count number printed when
                      restarting the program (unless it's a broken link, and in 
                      that case enter the next count number). 
    This is the scraper that scrapes multiple URLs from a given .txt file.
    '''
    urls = read_line(url_file)
    count = starting_url
    for i in range(starting_url, len(urls)):
        count += 1
        page_scraper(urls[i])
        print(count)
        
#THE FOLLOWING 3 FUNCTIONS ARE USED BY THE SCRAPER
        
def line_to_string(start, end, string, file):
    '''
    Parameters:
        start: starting index
        end: ending index
        string: a string that will be parsed 
        file: file where this parsed string will be written
    This function takes a string and writes a parsed string (from a given start
    and end index) into a given file.
    '''
    begin_index = string.find(start) + len(start)
    end_index = string.find(end, begin_index) 
    string_to_file(string[begin_index:end_index] + "\t", file)
    
def read_line(filename):
    '''
    Parameters:
        filename: a .txt file that has one item per line.
    Use this function to turn a .txt file that has one URL per line, into
    a list of URLs to be used by the scraper for the entire website.
    '''
    file = open(filename, 'r')
    lines = []
    for line in file:
        lines.append(line.strip())
    file.close()
    return lines 
    
def string_to_file(string, file):
    '''
    This writes a given string to a given file.
    '''
    out = open(file, "a")
    out.write(string)
    out.close()
