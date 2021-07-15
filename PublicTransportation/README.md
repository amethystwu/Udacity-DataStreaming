<p><a href="https://img.shields.io/badge/project-passed-success.svg" rel="nofollow"><img src="https://camo.githubusercontent.com/f4fa6834fb699c495aca3290c0f1a4169a9881d0a9309ad789e96562eaf00d82/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f70726f6a6563742d7061737365642d737563636573732e737667" alt="Project passed" data-canonical-src="https://img.shields.io/badge/project-passed-success.svg" style="max-width:100%;"></a></p>
<p>In this project, you will construct a streaming event pipeline around Apache Kafka and its ecosystem. Using public data from the <a href="https://www.transitchicago.com/data/" rel="nofollow">Chicago Transit Authority</a> we will construct an event pipeline around Kafka that allows us to simulate and display the status of train lines in real time.</p>
<p>When the project is complete, you will be able to monitor a website to watch trains move from station to station.</p>
<p><a target="_blank" rel="noopener noreferrer" href="https://github.com/amethystwu/Udacity-DataStreaming/blob/main/PublicTransportation/images/ui.png"><img src="https://github.com/amethystwu/Udacity-DataStreaming/blob/main/PublicTransportation/images/ui.png" alt="Final User Interface" style="max-width:100%;"></a></p>
<h2><a id="user-content-prerequisites" class="anchor" aria-hidden="true" href="#prerequisites"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Prerequisites</h2>
<p>The following are required to complete this project:</p>
<ul>
<li>Docker</li>
<li>Python 3.7</li>
<li>Access to a computer with a minimum of 16gb+ RAM and a 4-core CPU to execute the simulation</li>
</ul>
<h2><a id="user-content-description" class="anchor" aria-hidden="true" href="#description"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Description</h2>
<p>The Chicago Transit Authority (CTA) has asked us to develop a dashboard displaying system status for its commuters. We have decided to use Kafka and ecosystem tools like REST Proxy and Kafka Connect to accomplish this task.</p>
<p>Our architecture will look like so:</p>
<p><a target="_blank" rel="noopener noreferrer" href="https://github.com/amethystwu/Udacity-DataStreaming/blob/main/PublicTransportation/images/diagram.png"><img src="https://github.com/amethystwu/Udacity-DataStreaming/blob/main/PublicTransportation/images/diagram.png" alt="Project Architecture" style="max-width:100%;"></a></p>
<h3><a id="user-content-step-1-create-kafka-producers" class="anchor" aria-hidden="true" href="#step-1-create-kafka-producers"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Step 1: Create Kafka Producers</h3>
<p>The first step in our plan is to configure the train stations to emit some of the events that we need. The CTA has placed a sensor on each side of every train station that can be programmed to take an action whenever a train arrives at the station.</p>
<p>To accomplish this, you must complete the following tasks:</p>
<ol>
<li>Complete the code in <code>producers/models/producer.py</code></li>
<li>Define a <code>value</code> schema for the arrival event in <code>producers/models/schemas/arrival_value.json</code> with the following attributes
<ul>
<li><code>station_id</code></li>
<li><code>train_id</code></li>
<li><code>direction</code></li>
<li><code>line</code></li>
<li><code>train_status</code></li>
<li><code>prev_station_id</code></li>
<li><code>prev_direction</code></li>
</ul>
</li>
<li>Complete the code in <code>producers/models/station.py</code> so that:
<ul>
<li>A topic is created for each station in Kafka to track the arrival events</li>
<li>The station emits an <code>arrival</code> event to Kafka whenever the <code>Station.run()</code> function is called.</li>
<li>Ensure that events emitted to kafka are paired with the Avro <code>key</code> and <code>value</code> schemas</li>
</ul>
</li>
<li>Define a <code>value</code> schema for the turnstile event in <code>producers/models/schemas/turnstile_value.json</code> with the following attributes
<ul>
<li><code>station_id</code></li>
<li><code>station_name</code></li>
<li><code>line</code></li>
</ul>
</li>
<li>Complete the code in <code>producers/models/turnstile.py</code> so that:
<ul>
<li>A topic is created for each turnstile for each station in Kafka to track the turnstile events</li>
<li>The station emits a <code>turnstile</code> event to Kafka whenever the <code>Turnstile.run()</code> function is called.</li>
<li>Ensure that events emitted to kafka are paired with the Avro <code>key</code> and <code>value</code> schemas</li>
</ul>
</li>
</ol>
<h3><a id="user-content-step-2-configure-kafka-rest-proxy-producer" class="anchor" aria-hidden="true" href="#step-2-configure-kafka-rest-proxy-producer"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Step 2: Configure Kafka REST Proxy Producer</h3>
<p>Our partners at the CTA have asked that we also send weather readings into Kafka from their weather hardware. Unfortunately, this hardware is old and we cannot use the Python Client Library due to hardware restrictions. Instead, we are going to use HTTP REST to send the data to Kafka from the hardware using Kafka's REST Proxy.</p>
<p>To accomplish this, you must complete the following tasks:</p>
<ol>
<li>Define a <code>value</code> schema for the weather event in <code>producers/models/schemas/weather_value.json</code> with the following attributes
<ul>
<li><code>temperature</code></li>
<li><code>status</code></li>
</ul>
</li>
<li>Complete the code in <code>producers/models/weather.py</code> so that:
<ul>
<li>A topic is created for weather events</li>
<li>The weather model emits <code>weather</code> event to Kafka REST Proxy whenever the <code>Weather.run()</code> function is called.
<ul>
<li><strong>NOTE</strong>: When sending HTTP requests to Kafka REST Proxy, be careful to include the correct <code>Content-Type</code>. Pay close attention to the <a href="https://docs.confluent.io/current/kafka-rest/api.html#post--topics-(string-topic_name)" rel="nofollow">examples in the documentation</a> for more information.</li>
</ul>
</li>
<li>Ensure that events emitted to REST Proxy are paired with the Avro <code>key</code> and <code>value</code> schemas</li>
</ul>
</li>
</ol>
<h3><a id="user-content-step-3-configure-kafka-connect" class="anchor" aria-hidden="true" href="#step-3-configure-kafka-connect"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Step 3: Configure Kafka Connect</h3>
<p>Finally, we need to extract station information from our PostgreSQL database into Kafka. We've decided to use the <a href="https://docs.confluent.io/current/connect/kafka-connect-jdbc/source-connector/index.html" rel="nofollow">Kafka JDBC Source Connector</a>.</p>
<p>To accomplish this, you must complete the following tasks:</p>
<ol>
<li>Complete the code and configuration in <code>producers/connectors.py</code>
<ul>
<li>Please refer to the <a href="https://docs.confluent.io/current/connect/kafka-connect-jdbc/source-connector/source_config_options.html" rel="nofollow">Kafka Connect JDBC Source Connector Configuration Options</a> for documentation on the options you must complete.</li>
<li>You can run this file directly to test your connector, rather than running the entire simulation.</li>
<li>Make sure to use the <a href="http://localhost:8084" rel="nofollow">Landoop Kafka Connect UI</a> and <a href="http://localhost:8085" rel="nofollow">Landoop Kafka Topics UI</a> to check the status and output of the Connector.</li>
<li>To delete a misconfigured connector: <code>CURL -X DELETE localhost:8083/connectors/stations</code></li>
</ul>
</li>
</ol>
<h3><a id="user-content-step-4-configure-the-faust-stream-processor" class="anchor" aria-hidden="true" href="#step-4-configure-the-faust-stream-processor"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Step 4: Configure the Faust Stream Processor</h3>
<p>We will leverage Faust Stream Processing to transform the raw Stations table that we ingested from Kafka Connect. The raw format from the database has more data than we need, and the line color information is not conveniently configured. To remediate this, we're going to ingest data from our Kafka Connect topic, and transform the data.</p>
<p>To accomplish this, you must complete the following tasks:</p>
<ol>
<li>Complete the code and configuration in `consumers/faust_stream.py</li>
</ol>
<h4><a id="user-content-watch-out" class="anchor" aria-hidden="true" href="#watch-out"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Watch Out!</h4>
<p>You must run this Faust processing application with the following command:</p>
<p><code>faust -A faust_stream worker -l info</code></p>
<h3><a id="user-content-step-5-configure-the-ksql-table" class="anchor" aria-hidden="true" href="#step-5-configure-the-ksql-table"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Step 5: Configure the KSQL Table</h3>
<p>Next, we will use KSQL to aggregate turnstile data for each of our stations. Recall that when we produced turnstile data, we simply emitted an event, not a count. What would make this data more useful would be to summarize it by station so that downstream applications always have an up-to-date count</p>
<p>To accomplish this, you must complete the following tasks:</p>
<ol>
<li>Complete the queries in <code>consumers/ksql.py</code></li>
</ol>
<h4><a id="user-content-tips" class="anchor" aria-hidden="true" href="#tips"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Tips</h4>
<ul>
<li>The KSQL CLI is the best place to build your queries. Try <code>ksql</code> in your workspace to enter the CLI.</li>
<li>You can run this file on its own simply by running <code>python ksql.py</code></li>
<li>Made a mistake in table creation? <code>DROP TABLE &lt;your_table&gt;</code>. If the CLI asks you to terminate a running query, you can <code>TERMINATE &lt;query_name&gt;</code></li>
</ul>
<h3><a id="user-content-step-6-create-kafka-consumers" class="anchor" aria-hidden="true" href="#step-6-create-kafka-consumers"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Step 6: Create Kafka Consumers</h3>
<p>With all of the data in Kafka, our final task is to consume the data in the web server that is going to serve the transit status pages to our commuters.</p>
<p>To accomplish this, you must complete the following tasks:</p>
<ol>
<li>Complete the code in <code>consumers/consumer.py</code></li>
<li>Complete the code in <code>consumers/models/line.py</code></li>
<li>Complete the code in <code>consumers/models/weather.py</code></li>
<li>Complete the code in <code>consumers/models/station.py</code></li>
</ol>
<h3><a id="user-content-documentation" class="anchor" aria-hidden="true" href="#documentation"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Documentation</h3>
<p>In addition to the course content you have already reviewed, you may find the following examples and documentation helpful in completing this assignment:</p>
<ul>
<li><a href="https://docs.confluent.io/current/clients/confluent-kafka-python/#" rel="nofollow">Confluent Python Client Documentation</a></li>
<li><a href="https://github.com/confluentinc/confluent-kafka-python#usage">Confluent Python Client Usage and Examples</a></li>
<li><a href="https://docs.confluent.io/current/kafka-rest/api.html#post--topics-(string-topic_name)" rel="nofollow">REST Proxy API Reference</a></li>
<li><a href="https://docs.confluent.io/current/connect/kafka-connect-jdbc/source-connector/source_config_options.html" rel="nofollow">Kafka Connect JDBC Source Connector Configuration Options</a></li>
</ul>
<h2><a id="user-content-directory-layout" class="anchor" aria-hidden="true" href="#directory-layout"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Directory Layout</h2>
<p>The project consists of two main directories, <code>producers</code> and <code>consumers</code>.</p>
<p>The following directory layout indicates the files that the student is responsible for modifying by adding a <code>*</code> indicator. Instructions for what is required are present as comments in each file.</p>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="* - Indicates that the student must complete the code in this file

├── consumers
│   ├── consumer.py *
│   ├── faust_stream.py *
│   ├── ksql.py *
│   ├── models
│   │   ├── lines.py
│   │   ├── line.py *
│   │   ├── station.py *
│   │   └── weather.py *
│   ├── requirements.txt
│   ├── server.py
│   ├── topic_check.py
│   └── templates
│       └── status.html
└── producers
    ├── connector.py *
    ├── models
    │   ├── line.py
    │   ├── producer.py *
    │   ├── schemas
    │   │   ├── arrival_key.json
    │   │   ├── arrival_value.json *
    │   │   ├── turnstile_key.json
    │   │   ├── turnstile_value.json *
    │   │   ├── weather_key.json
    │   │   └── weather_value.json *
    │   ├── station.py *
    │   ├── train.py
    │   ├── turnstile.py *
    │   ├── turnstile_hardware.py
    │   └── weather.py *
    ├── requirements.txt
    └── simulation.py
"><pre><code>* - Indicates that the student must complete the code in this file

├── consumers
│   ├── consumer.py *
│   ├── faust_stream.py *
│   ├── ksql.py *
│   ├── models
│   │   ├── lines.py
│   │   ├── line.py *
│   │   ├── station.py *
│   │   └── weather.py *
│   ├── requirements.txt
│   ├── server.py
│   ├── topic_check.py
│   └── templates
│       └── status.html
└── producers
    ├── connector.py *
    ├── models
    │   ├── line.py
    │   ├── producer.py *
    │   ├── schemas
    │   │   ├── arrival_key.json
    │   │   ├── arrival_value.json *
    │   │   ├── turnstile_key.json
    │   │   ├── turnstile_value.json *
    │   │   ├── weather_key.json
    │   │   └── weather_value.json *
    │   ├── station.py *
    │   ├── train.py
    │   ├── turnstile.py *
    │   ├── turnstile_hardware.py
    │   └── weather.py *
    ├── requirements.txt
    └── simulation.py
</code></pre></div>
<h2><a id="user-content-running-and-testing" class="anchor" aria-hidden="true" href="#running-and-testing"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Running and Testing</h2>
<p>To run the simulation, you must first start up the Kafka ecosystem on their machine utilizing Docker Compose.</p>
<p><code>%&gt; docker-compose up</code></p>
<p>Docker compose will take a 3-5 minutes to start, depending on your hardware. Please be patient and wait for the docker-compose logs to slow down or stop before beginning the simulation.</p>
<p>Once docker-compose is ready, the following services will be available:</p>
<table>
<thead>
<tr>
<th>Service</th>
<th>Host URL</th>
<th>Docker URL</th>
<th>Username</th>
<th>Password</th>
</tr>
</thead>
<tbody>
<tr>
<td>Public Transit Status</td>
<td><a href="http://localhost:8888" rel="nofollow">http://localhost:8888</a></td>
<td>n/a</td>
<td></td>
<td></td>
</tr>
<tr>
<td>Landoop Kafka Connect UI</td>
<td><a href="http://localhost:8084" rel="nofollow">http://localhost:8084</a></td>
<td><a href="http://connect-ui:8084" rel="nofollow">http://connect-ui:8084</a></td>
<td></td>
<td></td>
</tr>
<tr>
<td>Landoop Kafka Topics UI</td>
<td><a href="http://localhost:8085" rel="nofollow">http://localhost:8085</a></td>
<td><a href="http://topics-ui:8085" rel="nofollow">http://topics-ui:8085</a></td>
<td></td>
<td></td>
</tr>
<tr>
<td>Landoop Schema Registry UI</td>
<td><a href="http://localhost:8086" rel="nofollow">http://localhost:8086</a></td>
<td><a href="http://schema-registry-ui:8086" rel="nofollow">http://schema-registry-ui:8086</a></td>
<td></td>
<td></td>
</tr>
<tr>
<td>Kafka</td>
<td>PLAINTEXT://localhost:9092,PLAINTEXT://localhost:9093,PLAINTEXT://localhost:9094</td>
<td>PLAINTEXT://kafka0:9092,PLAINTEXT://kafka1:9093,PLAINTEXT://kafka2:9094</td>
<td></td>
<td></td>
</tr>
<tr>
<td>REST Proxy</td>
<td><a href="http://localhost:8082/" rel="nofollow">http://localhost:8082</a></td>
<td><a href="http://rest-proxy:8082/" rel="nofollow">http://rest-proxy:8082/</a></td>
<td></td>
<td></td>
</tr>
<tr>
<td>Schema Registry</td>
<td><a href="http://localhost:8081/" rel="nofollow">http://localhost:8081</a></td>
<td><a href="http://schema-registry:8081/" rel="nofollow">http://schema-registry:8081/</a></td>
<td></td>
<td></td>
</tr>
<tr>
<td>Kafka Connect</td>
<td><a href="http://localhost:8083" rel="nofollow">http://localhost:8083</a></td>
<td><a href="http://kafka-connect:8083" rel="nofollow">http://kafka-connect:8083</a></td>
<td></td>
<td></td>
</tr>
<tr>
<td>KSQL</td>
<td><a href="http://localhost:8088" rel="nofollow">http://localhost:8088</a></td>
<td><a href="http://ksql:8088" rel="nofollow">http://ksql:8088</a></td>
<td></td>
<td></td>
</tr>
<tr>
<td>PostgreSQL</td>
<td><code>jdbc:postgresql://localhost:5432/cta</code></td>
<td><code>jdbc:postgresql://postgres:5432/cta</code></td>
<td><code>cta_admin</code></td>
<td><code>chicago</code></td>
</tr>
</tbody>
</table>
<p>Note that to access these services from your own machine, you will always use the <code>Host URL</code> column.</p>
<p>When configuring services that run within Docker Compose, like <strong>Kafka Connect you must use the Docker URL</strong>. When you configure the JDBC Source Kafka Connector, for example, you will want to use the value from the <code>Docker URL</code> column.</p>
<h3><a id="user-content-running-the-simulation" class="anchor" aria-hidden="true" href="#running-the-simulation"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Running the Simulation</h3>
<p>There are two pieces to the simulation, the <code>producer</code> and <code>consumer</code>. As you develop each piece of the code, it is recommended that you only run one piece of the project at a time.</p>
<p>However, when you are ready to verify the end-to-end system prior to submission, it is critical that you open a terminal window for each piece and run them at the same time. <strong>If you do not run both the producer and consumer at the same time you will not be able to successfully complete the project</strong>.</p>
<h4><a id="user-content-to-run-the-producer" class="anchor" aria-hidden="true" href="#to-run-the-producer"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>To run the <code>producer</code>:</h4>
<ol>
<li><code>cd producers</code></li>
<li><code>virtualenv venv</code></li>
<li><code>. venv/bin/activate</code></li>
<li><code>pip install -r requirements.txt</code></li>
<li><code>python simulation.py</code></li>
</ol>
<p>Once the simulation is running, you may hit <code>Ctrl+C</code> at any time to exit.</p>
<h4><a id="user-content-to-run-the-faust-stream-processing-application" class="anchor" aria-hidden="true" href="#to-run-the-faust-stream-processing-application"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>To run the Faust Stream Processing Application:</h4>
<ol>
<li><code>cd consumers</code></li>
<li><code>virtualenv venv</code></li>
<li><code>. venv/bin/activate</code></li>
<li><code>pip install -r requirements.txt</code></li>
<li><code>faust -A faust_stream worker -l info</code></li>
</ol>
<h4><a id="user-content-to-run-the-ksql-creation-script" class="anchor" aria-hidden="true" href="#to-run-the-ksql-creation-script"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>To run the KSQL Creation Script:</h4>
<ol>
<li><code>cd consumers</code></li>
<li><code>virtualenv venv</code></li>
<li><code>. venv/bin/activate</code></li>
<li><code>pip install -r requirements.txt</code></li>
<li><code>python ksql.py</code></li>
</ol>
<h4><a id="user-content-to-run-the-consumer" class="anchor" aria-hidden="true" href="#to-run-the-consumer"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>To run the <code>consumer</code>:</h4>
<p>** NOTE **: Do not run the consumer until you have reached Step 6!</p>
<ol>
<li><code>cd consumers</code></li>
<li><code>virtualenv venv</code></li>
<li><code>. venv/bin/activate</code></li>
<li><code>pip install -r requirements.txt</code></li>
<li><code>python server.py</code></li>
</ol>
<p>Once the server is running, you may hit <code>Ctrl+C</code> at any time to exit.</p>
</article>
  </div>

    </div>

  </readme-toc>

  

  <details class="details-reset details-overlay details-overlay-dark" id="jumpto-line-details-dialog">
    <summary data-hotkey="l" aria-label="Jump to line"></summary>
    <details-dialog class="Box Box--overlay d-flex flex-column anim-fade-in fast linejump" aria-label="Jump to line">
      <!-- '"` --><!-- </textarea></xmp> --></option></form><form class="js-jump-to-line-form Box-body d-flex" action="" accept-charset="UTF-8" method="get">
        <input class="form-control flex-auto mr-3 linejump-input js-jump-to-line-field" type="text" placeholder="Jump to line&hellip;" aria-label="Jump to line" autofocus>
        <button data-close-dialog="" type="submit" data-view-component="true" class="btn">
  
  Go
  

</button>
</form>    </details-dialog>
  </details>

    <div class="Popover anim-scale-in js-tagsearch-popover"
     hidden
     data-tagsearch-url="/dvu4/udacity-data-streaming-project-1/find-definition"
     data-tagsearch-ref="master"
     data-tagsearch-path="README.md"
     data-tagsearch-lang="Markdown"
     data-hydro-click="{&quot;event_type&quot;:&quot;code_navigation.click_on_symbol&quot;,&quot;payload&quot;:{&quot;action&quot;:&quot;click_on_symbol&quot;,&quot;repository_id&quot;:254073443,&quot;ref&quot;:&quot;master&quot;,&quot;language&quot;:&quot;Markdown&quot;,&quot;originating_url&quot;:&quot;https://github.com/dvu4/udacity-data-streaming-project-1/blob/master/README.md&quot;,&quot;user_id&quot;:11830611}}"
     data-hydro-click-hmac="9f33403b47007b723025f17b907451f34d5032c4b577fc47ed54d88545bc37bd">
  <div class="Popover-message Popover-message--large Popover-message--top-left TagsearchPopover mt-1 mb-4 mx-auto Box color-shadow-large">
    <div class="TagsearchPopover-content js-tagsearch-popover-content overflow-auto" style="will-change:transform;">
    </div>
  </div>
</div>


</div>



  </div>
</div>

    </main>
  </div>

  </div>

          
<div class="footer container-xl width-full p-responsive" role="contentinfo">
  <div class="position-relative d-flex flex-row-reverse flex-lg-row flex-wrap flex-lg-nowrap flex-justify-center flex-lg-justify-between pt-6 pb-2 mt-6 f6 color-text-secondary border-top color-border-secondary ">
    <ul class="list-style-none d-flex flex-wrap col-12 col-lg-5 flex-justify-center flex-lg-justify-between mb-2 mb-lg-0">
      <li class="mr-3 mr-lg-0">&copy; 2021 GitHub, Inc.</li>
        <li class="mr-3 mr-lg-0"><a href="https://docs.github.com/en/github/site-policy/github-terms-of-service" data-ga-click="Footer, go to terms, text:terms">Terms</a></li>
        <li class="mr-3 mr-lg-0"><a href="https://docs.github.com/en/github/site-policy/github-privacy-statement" data-ga-click="Footer, go to privacy, text:privacy">Privacy</a></li>
        <li class="mr-3 mr-lg-0"><a data-ga-click="Footer, go to security, text:security" href="https://github.com/security">Security</a></li>
        <li class="mr-3 mr-lg-0"><a href="https://www.githubstatus.com/" data-ga-click="Footer, go to status, text:status">Status</a></li>
        <li><a data-ga-click="Footer, go to help, text:Docs" href="https://docs.github.com">Docs</a></li>
    </ul>

    <a aria-label="Homepage" title="GitHub" class="footer-octicon d-none d-lg-block mx-lg-4" href="https://github.com">
      <svg aria-hidden="true" viewBox="0 0 16 16" version="1.1" data-view-component="true" height="24" width="24" class="octicon octicon-mark-github">
    <path fill-rule="evenodd" d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"></path>
</svg>
</a>
    <ul class="list-style-none d-flex flex-wrap col-12 col-lg-5 flex-justify-center flex-lg-justify-between mb-2 mb-lg-0">
        <li class="mr-3 mr-lg-0"><a href="https://support.github.com" data-ga-click="Footer, go to contact, text:contact">Contact GitHub</a></li>
        <li class="mr-3 mr-lg-0"><a href="https://github.com/pricing" data-ga-click="Footer, go to Pricing, text:Pricing">Pricing</a></li>
      <li class="mr-3 mr-lg-0"><a href="https://docs.github.com" data-ga-click="Footer, go to api, text:api">API</a></li>
      <li class="mr-3 mr-lg-0"><a href="https://services.github.com" data-ga-click="Footer, go to training, text:training">Training</a></li>
        <li class="mr-3 mr-lg-0"><a href="https://github.blog" data-ga-click="Footer, go to blog, text:blog">Blog</a></li>
        <li><a data-ga-click="Footer, go to about, text:about" href="https://github.com/about">About</a></li>
    </ul>
  </div>
  <div class="d-flex flex-justify-center pb-6">
    <span class="f6 color-text-tertiary"></span>
  </div>

  
</div>



  <div id="ajax-error-message" class="ajax-error-message flash flash-error" hidden>
    <svg aria-hidden="true" viewBox="0 0 16 16" version="1.1" data-view-component="true" height="16" width="16" class="octicon octicon-alert">
    <path fill-rule="evenodd" d="M8.22 1.754a.25.25 0 00-.44 0L1.698 13.132a.25.25 0 00.22.368h12.164a.25.25 0 00.22-.368L8.22 1.754zm-1.763-.707c.659-1.234 2.427-1.234 3.086 0l6.082 11.378A1.75 1.75 0 0114.082 15H1.918a1.75 1.75 0 01-1.543-2.575L6.457 1.047zM9 11a1 1 0 11-2 0 1 1 0 012 0zm-.25-5.25a.75.75 0 00-1.5 0v2.5a.75.75 0 001.5 0v-2.5z"></path>
</svg>
    <button type="button" class="flash-close js-ajax-error-dismiss" aria-label="Dismiss error">
      <svg aria-hidden="true" viewBox="0 0 16 16" version="1.1" data-view-component="true" height="16" width="16" class="octicon octicon-x">
    <path fill-rule="evenodd" d="M3.72 3.72a.75.75 0 011.06 0L8 6.94l3.22-3.22a.75.75 0 111.06 1.06L9.06 8l3.22 3.22a.75.75 0 11-1.06 1.06L8 9.06l-3.22 3.22a.75.75 0 01-1.06-1.06L6.94 8 3.72 4.78a.75.75 0 010-1.06z"></path>
</svg>
    </button>
    You can’t perform that action at this time.
  </div>

  <div class="js-stale-session-flash flash flash-warn flash-banner" hidden
    >
    <svg aria-hidden="true" viewBox="0 0 16 16" version="1.1" data-view-component="true" height="16" width="16" class="octicon octicon-alert">
    <path fill-rule="evenodd" d="M8.22 1.754a.25.25 0 00-.44 0L1.698 13.132a.25.25 0 00.22.368h12.164a.25.25 0 00.22-.368L8.22 1.754zm-1.763-.707c.659-1.234 2.427-1.234 3.086 0l6.082 11.378A1.75 1.75 0 0114.082 15H1.918a1.75 1.75 0 01-1.543-2.575L6.457 1.047zM9 11a1 1 0 11-2 0 1 1 0 012 0zm-.25-5.25a.75.75 0 00-1.5 0v2.5a.75.75 0 001.5 0v-2.5z"></path>
</svg>
    <span class="js-stale-session-flash-signed-in" hidden>You signed in with another tab or window. <a href="">Reload</a> to refresh your session.</span>
    <span class="js-stale-session-flash-signed-out" hidden>You signed out in another tab or window. <a href="">Reload</a> to refresh your session.</span>
  </div>
    <template id="site-details-dialog">
  <details class="details-reset details-overlay details-overlay-dark lh-default color-text-primary hx_rsm" open>
    <summary role="button" aria-label="Close dialog"></summary>
    <details-dialog class="Box Box--overlay d-flex flex-column anim-fade-in fast hx_rsm-dialog hx_rsm-modal">
      <button class="Box-btn-octicon m-0 btn-octicon position-absolute right-0 top-0" type="button" aria-label="Close dialog" data-close-dialog>
        <svg aria-hidden="true" viewBox="0 0 16 16" version="1.1" data-view-component="true" height="16" width="16" class="octicon octicon-x">
    <path fill-rule="evenodd" d="M3.72 3.72a.75.75 0 011.06 0L8 6.94l3.22-3.22a.75.75 0 111.06 1.06L9.06 8l3.22 3.22a.75.75 0 11-1.06 1.06L8 9.06l-3.22 3.22a.75.75 0 01-1.06-1.06L6.94 8 3.72 4.78a.75.75 0 010-1.06z"></path>
</svg>
      </button>
      <div class="octocat-spinner my-6 js-details-dialog-spinner"></div>
    </details-dialog>
  </details>
</template>

    <div class="Popover js-hovercard-content position-absolute" style="display: none; outline: none;" tabindex="0">
  <div class="Popover-message Popover-message--bottom-left Popover-message--large Box color-shadow-large" style="width:360px;">
  </div>
</div>

    <template id="snippet-clipboard-copy-button">
  <div class="zeroclipboard-container position-absolute right-0 top-0">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w">
      <svg aria-hidden="true" viewBox="0 0 16 16" version="1.1" data-view-component="true" height="16" width="16" class="octicon octicon-clippy js-clipboard-clippy-icon m-2">
    <path fill-rule="evenodd" d="M5.75 1a.75.75 0 00-.75.75v3c0 .414.336.75.75.75h4.5a.75.75 0 00.75-.75v-3a.75.75 0 00-.75-.75h-4.5zm.75 3V2.5h3V4h-3zm-2.874-.467a.75.75 0 00-.752-1.298A1.75 1.75 0 002 3.75v9.5c0 .966.784 1.75 1.75 1.75h8.5A1.75 1.75 0 0014 13.25v-9.5a1.75 1.75 0 00-.874-1.515.75.75 0 10-.752 1.298.25.25 0 01.126.217v9.5a.25.25 0 01-.25.25h-8.5a.25.25 0 01-.25-.25v-9.5a.25.25 0 01.126-.217z"></path>
</svg>
      <svg aria-hidden="true" viewBox="0 0 16 16" version="1.1" data-view-component="true" height="16" width="16" class="octicon octicon-check js-clipboard-check-icon color-text-success d-none m-2">
    <path fill-rule="evenodd" d="M13.78 4.22a.75.75 0 010 1.06l-7.25 7.25a.75.75 0 01-1.06 0L2.22 9.28a.75.75 0 011.06-1.06L6 10.94l6.72-6.72a.75.75 0 011.06 0z"></path>
</svg>
    </clipboard-copy>
  </div>
</template>



  

  </body>
</html>

