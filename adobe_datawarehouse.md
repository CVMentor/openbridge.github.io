<h1>Setting Up Adobe Data Warehouse Feeds (AWF)</h1>
<h2>Overview</h2>
<p> The datawarehouse extract process enables Adobe customers a mechanism to export data from their account to an external location. The process of defining the extracts and sceduling delivery occurs within the Adobe website. You can generate ad hoc data reports on your historical reporting data, which are delivered as CSV files via FTP. You build a query to filter your data and isolate specific feeds. The vast majority of requests take less than a day to process, but depending on the complexity of your query and the amount of data it can take longer to process.

<p>The process outlined in this document described how to configure Openbridge to automate reception of those feeds, processing them and load them into a database.

<p> Please consult the Adobe website for the latest steps to configure feeds: <a href="https://marketing.adobe.com/developer/documentation/data-warehouse/c-data-warehouse-api">https://marketing.adobe.com/developer/documentation/data-warehouse/c-data-warehouse-api</a>
<p> Also, see <a href="file_transfer.html">Batch File Transfers</a> for additional context on the Adobe Datawarehouse Feed process. <a href="file_transfer.html">Batch File Transfers</a>  describes the additional cosniderations and requirements for feeds into Openbridge.

<h3>Delivery Endpoints</h3>

<p>Adobe defaults delivery to FTP. If you want to use SFTP, it will require a special request to the Adobe support team to setup.

<p>Delivery of files to the following
<ul>
<li>FTP Hostname = <code>ftp.openbridge.io</code>
<li>SFTP Hostname = <code>sftp.openbridge.io</code>
</ul>

<p>The following are the PORT numbers you will need to make sure are used by the system responsible for file delivery
<ul>
<li>FTP = <code>port:21</code>
<li>SFTP = <code>port:2222</code>
</ul>

<h3>Delivery Directory and Filemasks</h3>

<p>Feeds must have specific directories on the Openbridge system that correspond to each reporting suite. The output from Adobe should be delivered to a unique desitnation and use a filemask that corresponds to the report suite and report type being sent. For example:<br>
<code>"../(report_suite_id)//(report_type)/(report_type_YYYY-mm-dd).csv"</code>

<p>This would result in a unique desitnation and filemask would like something like this: <code>"../my-suite-id/adob_site_totals/adob_site_totals_20150101.csv"</code>

<p> This process would be repeated for each unique report type you want to have loaded. For example;
<br>
<code>
../my-suite-id/adob_channel/adob_channel_20150101.csv<br>
../my-suite-id/adob_pages/adob_pages_20150101.csv<br>
../my-suite-id/adob_products/adob_products_20150101.csv<br>
../my-suite-id/adob_site_totals/adob_site_totals_20150101.csv<br>
../my-suite-id/adob_video/adob_video_20150101.csv<br>
../my-suite-id/adob_visits/adob_visits_20150101.csv
</code>

<p>The root directory for Adobe Datawarehouse feeds would be: <code>/adobe/sitecatalyst/datawarehouse/..</code>.

<p>Report suite, report type and file are located in sub directories of this root. Here is an exmaple of the full path to a delivered file;<br>
<code>/adobe/sitecatalyst/datawarehouse/my-suite-id/adob_visits/adob_visits_20150101.csv</code>

<p>You typically will not need to worry about the root directory. The account credentials supplied to Adobe will drop the connection directly into the root of the datawarehouse folder. For example;<br>
<code>
/adobe/sitecatalyst/datawarehouse/(you are here)
</code>

<h3>Datawarehouse Feed Contents</h3>

<p>The delivery format from Adobe will be uncompressed CSV files. The raw files from Adobe will have headers that look like this:
<br>
<code>
| Date  | Visits | Unique Visitors | Something (23) (event23) |
</code>

<p>The headers as supplied are technically not valid for import into a database like Redshfit. In above example there are mixed case, special characters and spacing used for column names. Our system will automatically standardize the headers supplied by Adobe to ensure that downstream databses can properly import the data.

<p> The resulting header would look something like this:
<br>
<code>
 | date  | visits | unique_visitors | something_23_event23 |
</code>

<p> The values assocaited with the header follow typical CSV conventions:
<br>
<code>"January 1, 2015",111292,12513,8139</code>

<h3>Database Loading</h3>

<p> Once the direcotries have been configured and delivery from Adobe has commenced each day delivery of feeds will arrive/ For example;<br>
<code>"../my-suite-id/adob_site_totals/adob_site_totals_20150101.csv"</code><br>
<code>"../my-suite-id/adob_site_totals/adob_site_totals_20150102.csv"</code><br>
<code>"../my-suite-id/adob_site_totals/adob_site_totals_20150103.csv"</code>

<p> The system will proceess each CSV file according to the organizational structure the files are being delivered. For example, based on the above structure a table would be created called <code>adob_site_totals</code>. This is based on the report type directory name.

<p>Based on the header of the CSV file residing in the report type folder <code>adob_site_totals</code> columns would be created. In this example, the CSV contained the header <code>date, visits, unique_visitors, something_23_event23</code> would result in columns for each of those volumes.

<p>The CSV file will have values that would align to those headers. In this example the CSV file has follwoing values <code>"January 8, 2015",111292,12513,8139</code> assocaited with each header item <code>date, visits, unique_visitors, something_23_event23</code>. Those values would be loaded into a rown within the defined table.

<p>With each subsequent file delivery of for the <code>adob_site_totals</code> report suite the same process would occur.
<code>date,visits,unique_visitors,something_23_event23</code><br>
<code>"January 1, 2015",111292,3256,2243</code><br>
<code>"January 2, 2015",171540,12385,5654</code><br>
<code>"January 3, 2015",131791,23423,8453</code><br>
<code>"January 4, 2015",81292,4513,1296</code>


<h3>Access Credentials</h3>
<p>Adobe supports standard username and password credential for both FTP and SFTP. Openbridge will supply these to you to supply to Adobe technical support team. Adobe will only have access to the specific directory path mentioned previously. They are "locked" there and only have access to deliver files to the target directory.

<h3>Delivery Frequency</h3>
<p>You have the option of scheduling the frequency of your data warehouse with the Adobe website. We suggest that the feeds are scheduled daily, delivered between 3AM and 6AM daily.

<h3>
<a name="support-or-contact" class="anchor" href="#support-or-contact"><span class="octicon octicon-link"></span></a>Support or Contact</h3>

<p>Having trouble with something? Contact us at <a href="http://openbridge.zendesk.com">http://openbridge.zendesk.com</a> or contact <a href="mailto:support@openbridge.com">support@openbridge.com</a> and we’ll help you sort it out.</p>