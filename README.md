Download Link: https://assignmentchef.com/product/solved-comp250-assignment-2-a-confusing-train-ride
<br>
Due to a significant increase in its student population, especially in its Machine Learning department, the single direct train going to Hogwarts has been replaced by a network of 15 stations distributed over three lines. However, this has revealed to not exactly be an improvement. Just like the staircases within the castle, the stations get bored and, to fight this boredom, rearrange themselves every 2 hours. However, luckily for you, the stations have not yet started switching lines; they always remain on the same line, but the order of the stations within a line gets shuffled.

Your task is to implement this shuffling train network and simulate the trip of an unfortunate traveler. You will be given Java templates to complete. Follow the instructions for each class closely.

Here are a few things you should know about the network:

<ul>

 <li>Traveling between two stations takes an hour.</li>

 <li>All stations are unique and only exist on one line.</li>

 <li>Transfer is possible between specific stations of different lines, which are indicated by having the same name but followed by a unique letter, identifying a distinct platform. Those remain two distinct stations, but that offer the possibility of traveling from one to the other. Transfer is always two-way; if it is possible to transfer from station A to B, then transfer is possible from station B to A.</li>

 <li>If transferring is possible, the passenger is forced to transfer, unless the passenger would be transferring to a station he just transferred from. for example, if I station from station London – A to London – B, your next step is not to transfer from London – B to London – A.</li>

 <li>Shuffling occurs every two hours. During a shuffling event, the order of the stations within a line changes. The left and right terminals might change. The transfer stations are part of the shuffling, but they stations they transfer to remain unaffected.</li>

 <li>You can assume there is only one traveler on the network at a time, and that every line has a single train which is magically waiting for the traveler at the appropriate transfer station.</li>

</ul>

You should now be ready to start the assignment, which is divided in four classes, as follows:

First, you are given a class TrainStation. A TrainStation encodes the stations of the network. A station is part of a TrainLine, which you can imagine as a doubly linked list. It has the following fields:

<ul>

 <li>TrainStation left : the next station on the left</li>

 <li>TrainStation right : the next station on the right</li>

 <li>boolean rightTerminal : true if the station is at the right end of the line</li>

 <li>boolean leftTerminal : true if the station is at the left end of the line</li>

 <li>String name : the name of the station.</li>

 <li>TrainLine line: the TrainLine this station belongs to.</li>

 <li>boolean hasConnection: true if the train station connects to another line. This is the only public field.</li>

 <li>TrainStation transfersToStation : the station object on the other line, if this transfer exists.</li>

 <li>TrainLine transfersToLine : the line object you can transfer to at this station.</li>

</ul>

All those fields, except hasConnection, are private. As such, you are provided with get and set methods for all the private fields. The class also comes with two constructors, as well as an equals method for comparing stations. <strong>Do not modify the TrainStation class.</strong>

You are also given a class TrainLine. A TrainLine contains stations that move around. It has the following fields:

<ul>

 <li>TrainStation leftTerminus : the terminal station on the left • TrainStation rightTerminus : the terminal station on the right</li>

 <li>String lineName : the name of the line.</li>

 <li>boolean goingRight: true if the train is going from the left to the right (assuming node 0 is at the left, and the last node at the right). You can assume there is only one train on the line which magically awaits for you at the transfer station, so the direction of the line is the direction of this train.</li>

 <li>public TrainStation[] lineMap : an array of TrainStation which encodes the <em>map </em>of the line. in that array, the station at index 0 is the left-most station of the line.</li>

</ul>

A constructor is provided, as well as equals method and a helper class StationNotFoundException. You are also provided with a method toString which converts the lineMap to a String for printing purposes. Finally, a function shuffleArray shuffles the lineMap for you.

Your task is to implement the following methods:

<ul>

 <li>public int getSize() : this method returns an integer equal to the number of stations on the line.</li>

 <li>public TrainStation findStation(String name) : this method take as input the name of a station, and searches through the line to return the TrainStation of this name. All station names are unique.

  <ul>

   <li>Iterate over the line until you find a station of the right name.</li>

   <li>If the station is not found, throw a StationNotFoundException</li>

  </ul></li>

 <li>public TrainStation getNext(TrainStation station) : takes as input a station and returns the next station of the line.

  <ul>

   <li>There is only one train on the line, it always goes in the same direction, until it hits a terminal station, then it turns around.</li>

   <li>Use the goingRight field to know in which direction the train is going.</li>

   <li>if the station is not on this line, throw a StationNotFoundException.</li>

   <li><strong>You cannot use the lineMap to find the next station.</strong></li>

  </ul></li>

 <li>public TrainStation travelOneStation(TrainStation current, TrainStation previous) : takes as input the previous and the current station and returns the next station, but while also considering line transfers. Line transfers count as a station change and take the same time as a standard move between stations. So if you are at a station that has the option of transferring, travelOnestation should return the station transferred to, and this should count as one time step of one hour.

  <ul>

   <li>Trains do not like passengers. If you have the opportunity to transfer, you must, unless transferring brings you back to the station you just arrived from (condemning you to an eternal ping-pong between the two).</li>

   <li>If a valid transfer is available, return the station you transferred to. Otherwise, return the next station on the usual path of the line, computed with getNext.</li>

   <li>If the current argument to travelOneStation is not on this train line, throw a</li>

  </ul></li>

</ul>

StationNotFoundException

<strong>–</strong>

<ul>

 <li>public TrainStation[] getLineArray() : returns an array of the train stations on the line, in order from the left terminal (index 0 of the array) to the right terminal (last index of the array).</li>

 <li>public void shuffleLine() : shuffles the station on the line.

  <ul>

   <li>You are provided with a shuffleArray method, which takes as input an array of TrainStations generated with getLineArray, and updated the lineMap to a shuffled version of this array.</li>

   <li>Once you generated this shuffled array, reorder the stations of the line so that their order matches that of the lineMap.</li>

   <li>tips: remember to keep track of the terminal stations, and to update the TrainStation</li>

   <li>public void sortLine() : sorts the stations of the line in increasing alphabetical order, and updates the lineMap. Note that for clarity, we make every station name in TrainRide start with a number. Numbers are included in the alphabetical comparison. You can use any of the algorithms covered in class, namely bubble sort, insertion sort, or selection sort. No matter what you use, you need to implement it yourself. Tip: you can make a helper swap function to make your life easier.</li>

  </ul></li>

</ul>

You are also given a class TrainNetwork. A TrainNetwork contains an array of train lines. You are asked to implement the following functions:

<ul>

 <li>public TrainLine getLineByName(String lineName) : this method take as input the name of a Line and returns a line of that name, otherwise throws a LineNotFoundException (helper class provided).</li>

 <li>public void dance() : shuffles all the lines using shuffleLine.</li>

 <li>public void undance() : sorts all the lines using sortLine.</li>

 <li>public int travel(String startStation, String startLine, String endStation, String endLine) : the key function of the program. It takes as input coordinates for departure and arrival and simulates a trip. Please follow the instructions closely.

  <ol>

   <li>Obtain departure station and line objects from the name strings provided as parameters to the method. Store them in the variables curLine and curStation.</li>

   <li>Iterate over the train network starting at the departure station in the provided while loop, updating curStation and curLine . You can change the termination condition.</li>

   <li>Keep track of the number of stations visited. This number is equal to the number of hours spent on the train. Assume line transfers always take an hour.</li>

   <li>Remember the network dances every <strong>two </strong></li>

   <li>At each iteration, keep track of the current station and the previous station. Tip: you do need to keep track of the previous station even if it is not obvious why. Remember how transferring works.</li>

   <li>at each iteration, check whether you have arrived at destination by comparing the objective name to the name of the current station.</li>

   <li>Once you have reached the destination, or after 168 hours of traveling, stop iterating and return an integer equal to the number of hours spent traveling.</li>

   <li>If the station cannot be found, assume you stayed on the train for a week before giving up, and return 168.</li>

   <li>Do not throw exceptions in this method.</li>

  </ol></li>

</ul>

You are also provided with a pre-written class TrainRide, which instantiates the different objects to a full train network (see the illustration). You can make modifications to the lines or itinerary to test out your code,