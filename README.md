# Securing Automated Vehicles

Welcome to my repository, where we share our collective experiences in securing self-driving cars gleaned over the past few years across multiple roles. Despite the burgeoning interest in self-driving technology, there's a noticeable dearth of practical insights on its security. With this repository, I endeavour to fill this gap by offering foundational knowledge to both the public and fellow practitioners, aiming to advance the security of these cutting-edge vehicles.

Defining what constitutes a "self-driving" car can be a subjective endeavour, with varying interpretations impacting discussions on attack surfaces, threat models, and overall security. Our goal here is to address these ambiguities head-on, providing clarity on key concepts and practical approaches. While our coverage may not be exhaustive, we strive to offer insights into different self-driving car tiers, prevalent threat models, security architectures, and collaborative strategies to fortify the driverless revolution.

# Definitions of Self-Driving Cars

Navigating the realm of self-driving cars, also referred to as Autonomous Vehicles (AVs), often entails grappling with ambiguity. To bring clarity to the diverse landscape of self-driving technology, SAE International introduced the J3016 standard. This framework delineates six distinct levels of automation found in vehicles, providing a structured approach for classification. However, the classification of certain technologies can pose challenges, especially when they exhibit features spanning multiple categories. In such instances, we rely on the illustrative examples outlined by Car and Driver magazine 

# Level 0: No Automation

Describing vehicles devoid of automation technologies, Level 0 signifies that the driver retains complete control of the vehicle at all times. Think of cars reminiscent of those from two decades ago. Even a vehicle equipped with standard cruise control would fall under this classification, as per subsequent definitions.

# Level 1: Driver Assistance

At this stage, driver assistance encompasses technologies aiding the driver with either steering or speed control, albeit not simultaneously. The driver remains fully responsible for the vehicle and must maintain vigilance in monitoring the environment. Examples of such technologies include the Jeep Cherokee's Adaptive Cruise Control and Lane Keep Assist functionality.

# Level 2: Partial Automation

Here, the vehicle gains the capability to control steering, acceleration, and braking under specific conditions. Nevertheless, the driver bears the responsibility of environmental observation and may be prompted to reassume control at any moment. These vehicles typically issue reminders for the driver to keep hands on the wheel or eyes on the road. Examples include the Tesla Autopilot and Volvo Pilot Assist.

# Level 3: Conditional Automation

Under suitable conditions, Level 3 automation empowers the vehicle to manage all driving aspects, including environment monitoring. While human oversight remains necessary, the vehicle may prompt the driver and relinquish control if faced with a situation beyond its capability. Although the driver is relieved of direct vehicle control, they must be prepared to resume control promptly. An instance of this technology is the Audi Traffic Jam Pilot, featured in select 2019 Audi models.

# Level 4: High Automation

Level 4 vehicles exhibit the capacity to operate without a human driver within predefined areas restricted by road type or geography. Within these demarcated regions or roads, the vehicle assumes full operational responsibility without human intervention, potentially lacking features such as a steering wheel or operator pedals. Notable examples encompass the majority of "self-driving" cars currently undergoing piloting by companies like Cruise, Uber, and Waymo.
ChatGPT can make mistakes. Consider checking important information.
<img src="https://i0.wp.com/electrek.co/wp-content/uploads/sites/3/2022/07/Baidu-robotaxi-Hero.jpg?w=1500&quality=82&strip=all&ssl=1" width="500">

# Level 5: Full Automation

Representing the pinnacle of self-driving technology, Level 5 signifies complete autonomy, where the vehicle requires no human interaction and can navigate any road under any conditions. To contextualize, while Level 4 self-driving cars presently necessitate the compilation of high-resolution maps within specific areas before operation, Level 5 obviates the need for such preparations. Notably, there are currently no examples of vehicles attaining this level of autonomy, yet it stands as the ultimate objective for vehicle manufacturers.

# Use Cases

In addition to delineating levels of automation, self-driving cars serve various use cases. One primary scenario involves production vehicles tailored for sale to customers. These represent the conventional vehicles we encounter on roads today, enhanced with advanced autonomy features. As previously noted, vehicles with Level 4 or higher automation capabilities are currently unavailable for purchase. This scarcity may stem from factors like prohibitive costs, maintenance complexities, or other considerations. Nevertheless, most automotive manufacturers are believed to be in the process of developing such vehicles, albeit none are presently accessible to consumers.

Another category comprises ride-sharing vehicles, owned by companies but accessible to end users for transportation. Examples include vehicles manufactured and trialled'/ by entities like Uber, Waymo, and Cruise. These vehicles return to a designated garage each night for continual supervision, updates, and maintenance.

This repo focuses on the cybersecurity implications pertinent to the latter category of vehicles—those not owned by end users and equipped with Level 4 automation capabilities.

# The Current State of Self-Driving Cars

Before delving into the security considerations surrounding self-driving cars, it's essential to provide an overview of their current state. Understanding the timeline and pertinent details is crucial for assessing the urgency and requisite pace in fortifying these vehicles.

Waymo initiated its self-driving car development efforts as early as 2009 [3], marking less than a decade since the inception of this groundbreaking technology. Other industry players such as Uber and Cruise embarked on similar ventures several years later [4][5].

In many regions, regulations governing self-driving cars are either absent or nascent. Historically, vehicles with autonomous capabilities required a human driver behind the wheel, poised to intervene in emergencies. These individuals, often termed safety drivers, played a pivotal role in early autonomous vehicle trials. For instance, as of 2014, California regulations permitted self-driving cars with safety drivers [6].

Recent legislative changes signal a shifting landscape. In March 2018, Arizona passed legislation allowing autonomous vehicles to operate without a human driver, marking the first law enabling Level 4 and 5 autonomy [6]. Subsequently, California followed suit in May 2018, albeit with restrictions on pilot programs, mandating remote operator oversight and stringent safety protocols [7]. Notably, California regulations stipulate "industry best" protection against cyber-attacks for autonomous vehicles.

While some US states have embraced self-driving car initiatives, widespread adoption remains a distant prospect. When can we anticipate the proliferation of Level 4 or above autonomous vehicles on our roads? The trajectory suggests it will be some time before they constitute the majority.

To gauge the scale of current self-driving car fleets, industry reports provide valuable insights. Over the coming years, Waymo intends to acquire 62,000 Chrysler Pacifica Minivans, while Uber has agreed to purchase 24,000 Volvo XC90 SUVs [8][9]. Consequently, an estimated 100,000 self-driving cars may populate roads in the near future.

However, this figure pales in comparison to the 253 million conventional vehicles and 3 million Uber drivers in the US [10][11]. Nonetheless, as self-driving technology matures and automotive manufacturers introduce these vehicles to market, envisioning a future dominated by autonomous cars, especially in urban hubs, becomes plausible. Several manufacturers aim to offer Level 4 or 5 vehicles for purchase by 2021 or 2022 [12].

Yet, within existing self-driving fleets, deployment is concentrated in select locations. Waymo primarily operates in Mountain View, CA, and Phoenix, AZ, while Uber's self-driving vehicles are predominantly stationed in Pittsburgh, PA [13][14]. Similarly, most Cruise vehicles navigate the streets of downtown San Francisco.

It's crucial to recognize that self-driving cars in these programs log substantially more miles than typical user-owned vehicles. Waymo vehicles, for instance, have amassed 4 million miles, while Uber and Cruise vehicles have recorded 2 million and 500,000 miles, respectively [15]. In contrast, the average driver covers 12-16 thousand miles annually [16]. This disparity underscores the extensive testing conducted by self-driving car companies.

The magnitude of miles driven not only exposes vehicles to diverse scenarios but also underscores their adaptability in tackling complex challenges. Unlike human drivers who often avoid problematic areas, such as construction zones or densely populated areas, self-driving cars actively seek out such scenarios to refine their capabilities [17]. Therefore, while miles driven serve as a pivotal metric, they also reflect the depth and complexity of testing undertaken by self-driving car manufacturers.

# Introduction to Self-Driving Cars

In order to delve into the security aspect of self-driving cars, it's essential to grasp their operational mechanisms. It's worth noting, our attention is directed towards level 4 autonomous vehicles.

# Hardware Components

Self-driving cars are equipped with an array of hardware not typically found in traditional passenger vehicles. The most notable disparity lies in the increased number of sensors utilized by the self-driving system (further elaborated below). Nonetheless, certain sensors, such as cameras and radar, are present in luxury vehicles. For instance, the 2015 Jeep we examined featured radar for adaptive cruise control and a camera for lane-keeping assistance. However, self-driving cars often boast a more extensive sensor suite, with numerous high-resolution cameras. As depicted below, Uber vehicles are outfitted with seven cameras.
