## Chapter 1 - Architectural Concepts
* Trusted Cloud Initiative (TCI) Reference Model
  * Feference model for cloud providers allowing them to create holistic architecture that cloud customers can purchase and
  use with comfort and confidence
  
* NIST 800-53
  * guidance document w/ primary goal of ensuring appropriate security requirements and controls are applied to all US Federal government information management systems
  
* Managed Services Provider
  * IT service where customer dictates tech and operational procedures and external party executes administration and operations support contract
  
* FIPS 140-2
  * NIST document that lists accredited and outmoded cryptosystems

* Eucalyptus
  * Open source cloud computing and IaaS platform for enabling private clouds

* Cloud Service Broker (CSB)
  * intermediary between cloud service customers and CSPs to help select best provider for each customer
  
* Cloud Computing Reseller
  * company purchases hosting services from cloud server hosting or compute provider and resells to its own customers
  
* Business requirement
  * operational driver for decision making and input for risk management
  
* Cloud Access Security Broker (CASB)
  * 3rd party offering IAM to CSPs and cloud customers that comes with single sign-on, certificate management, and cryptographic key escrow
  
* Cloud bursting
  * augment internal private datacenter capabilities with managed services during time of increased demand

* Nonfunctional requirements
  * aspects of device or process that are not necessary for accomplishing business task but are desired or expected
  * EXAMPLE: salesperson's connection to corporate network is secure
  
* Functional requirements
  * performance aspects of the device or process that are necessary for business task to be accomplished
  * EXAMPLE: salesperson must be able to connect to corporate network remotely
  
* Cloud characteristics
  * elasticity
  * simplicity
  * scalability
  
* Cloud computing characteristics
  * broad network access
  * on-demand services
  * resource pooling
  * measured/metered service
  
## Chapter 2 - Design Requirements
* homomorphic encryption
  * process data in cloud while it is encrypted w/o having to decrypt

* Cloud Provider Securing Devices
  * all guest accounts are removed
  * all unused ports are closed
  * no default passwords remain
  * strong password policies
  * admin accounts secured and logged
  * unnecessary services are disabled
  * physical access severly limited and controlled
  * systems patched, maintained, updated according to vendor guidance
  
* Deal with risks
  * Avoid
  * Accept
  * Transfer
  * Mitigate
  
* Risk
  * likelihood an impact will be realized
  
* Dealing with Single Point of Failure (SPOF)
  * add redundancy
  * create alternative paths
  * crosstrain personnel
  * backups and restore
  * load sharing
  
* Business Impact Analysis (BIA)
  * determine value of each asset, cost to org if lost, cost to replace or repair, and method to deal with loss
  * used to identify SPOF
  
* Business requirements analysis
  * inventory of all assets
  * valuation of all assets
  * determination of critical paths, processes, and assets
  * understanding of risk appetite
  
## Chapter 3 - Data Classification
* Data classification
  * characteristics of data such as sensitivity, jurisdiction, or criticality

* Data Categorization
  * define how data is used
  
* Data Owner (Data Controller)
  * org that collected or created data
  * usually department head

* Data Custodian (Data Processor)
  * manipulates, stores, moves data on behalf of data owner
  
* Data discovery
  * create inventory of data it wons
  * ediscovery
  * datamining to discover trends and relations in data
  * label-based, metadata-based, and content-based

* Data Destruction / Disposal Policy Requirements [Destroy Phase]
  * process for data disposal
  * applicable regulations
  * clear direction of when data should be destroyed
  
* Data Audit Policy Requirements [All Phases]
  * Audit periods
  * Audit scope
  * Audit responsibilities
  * Audit processes and procedures
  * Applicable regulations
  * Monitoring, maintenance, enforcement

* Data Retention Policy Properties [Archive]
  * retention period
  * applicable regulation
  * retention formats
  * data classification
  * archiving and retrieval procedures
  * monitoring, maintenance, enforcement
  
* DRM Functional Requirements
  * persistent protection
  * dynamic policy control
  * automatic expiration
  * continuous auditing
  * replication restrictions
  * remote revocation
  
* Trade Secret
  * exists upon creation and are similar to patents
  * cannot be made public and must reasonably try to keep secret
  
* Patents
  * legal mechanism for protecting intellectual property in form of inventions, processes, materials, plant life
  * lasts about 20 years
  
* Trademarks
  * applied to specific words or graphics
  * must be registered w/ jurisdiction such as US Patent and Trademark Office (USPTO)
  * lasts forever as long as used for commercial purposes
  
* Copyright - Fair Use
  * academic
  * critique
  * news reporting
  * scholarly research
  
* Copyright
  * legal expression of ideas
  * granted to anyone who first creates expression of idea
  * film, music, etc
  * granted as soon as expression put into tangible medium
  
* Intellectual property
  * class of valuable belongings that are intangible
  
* Real-time analytics
  * determining functionality concurrently w/ data creation and use
  
* Agile business intelligence
  * state-of-the-art datamining where recursive, iterative tools and processes detect trends within trends to identify more oblique patterns in historical or recent data
  
* Datamining
  * org collects data streams and queries across data to detect and analyze previously unknown trends and patterns
  
* metadata
  * listing of traits and characteristics about data elements or sets
  
* Data Labels
  * indicates who data is
  * creation date, scheduled destruction
  * confidentiality level
  * access limitations
  * source
  * jurisdiction/applicable regulation


