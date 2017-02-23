<h1>Setting Up Adobe Clickstream Feeds</h1>
<h2>Overview</h2>

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

<p>Feeds must have specific directories on the Openbridge system that correspond to each reporting suite. For example, the delivery would be sent to the root of the report suite directory like this: <code>".../(report_suite_id)/..." </code>
</p>
<p>The actual delivery will be zipped would follow this convention for the path and filemask.: <code>"/(report_suite_id)/(report_suite_YYYY-mm-dd).tar.gz"</code>

<h3>Access Credentials</h3>
<p>Adobe supports standard username and password credential for both FTP and SFTP. Openbridge will supply these to you to supply to Adobe technical support team. Adobe will only have access to the specific directory path mentioned previously. They are "locked" there and only have access to deliver files to the target directory.

<h3>Delivery Frequency</h3>
<p>You have the option of requesting Daily Single or Daily Multiple for delivery. We suggest the delivery of a single, consolidated file each day. The clickstream feeds are typically delivered between 1AM and 4AM daily.



<h3>Clickstream Feed Contents</h3>
<p>We have provided public repository of samples of clickstream data feeds on Github: <a href="https://github.com/openbridge/adobe-clickstream">https://github.com/openbridge/adobe-clickstream</a>

<p>In addition to reviewing the same data we provided, we suggest you review the Adobe specs here: <a href="http://microsite.omniture.com/t2/help/en_US/sc/clickstream/index.html#Clickstream_Data">http://microsite.omniture.com/t2/help/en_US/sc/clickstream/index.html#Clickstream_Data</a>.

<p>If you are planning to use the full payload as defined Adobe there are consideration in complexity and storage volumes. This is due to the fact that there are in excess of 500 columns of data, each with varying lengths and data types. Each record will consume a sizable chunk of space.

<p>Take a look at Adobe's recommended subset of that superset of columns here: <a href="http://microsite.omniture.com/t2/help/en_US/sc/clickstream/index.html#Configuring_Data">http://microsite.omniture.com/t2/help/en_US/sc/clickstream/index.html#Configuring_Data_Feeds</a>


<h3>Lookup/Helper Files</h3>
<p>Contents of each zip file would contain the following;

<ol>
<li>column_headers.tsv

<li>browser.tsv

<li>browser_type.tsv

<li>color_depth.tsv

<li>connection_type.tsv

<li>country.tsv

<li>javascript_version.tsv

<li>languages.tsv

<li>operating_systems.tsv

<li>plugins.tsv

<li>resolution.tsv

<li>referrer_type.tsv

<li>search_engines.tsv

<li>event_lookup.tsv
</ol>




<h3>
<a name="support-or-contact" class="anchor" href="#support-or-contact"><span class="octicon octicon-link"></span></a>Support or Contact</h3>

<p>Having trouble with something? Contact us at <a href="http://openbridge.zendesk.com">http://openbridge.zendesk.com</a> or contact <a href="mailto:support@openbridge.com">support@openbridge.com</a> and we’ll help you sort it out.</p>