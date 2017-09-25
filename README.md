# Queue
Queues can be implemented in JavaScript using arrays, by using the push or unshift functions to add items to one end of the array, and the shift or pop functions to remove them from the other. This method, while simple, is inefficient for large queues as the shift and unshift functions move every item in the array.
## Simple Queue
```
function Queue() {
    var items = [];
    this.enqueue = function (element) {
        items.push(element);
    }
    this.dequeue = function () {
        return items.shift();
    }
    this.front = function () {
        return items[0];
    }
    this.isEmpty = function () {
        return items.length == 0;
    }
    this.size = function () {
        return items.length;
    }
    this.print = function () {
        console.log(items.toString());
    }
    this.get = function () {
        return items;
    }
}

var queue = new Queue();
console.log(queue.isEmpty());
queue.enqueue("John");
queue.enqueue("Jack");
queue.enqueue("Camila");

queue.print();
console.log(queue.size());
console.log(queue.isEmpty());
queue.dequeue();
queue.dequeue();
queue.print();

```
## The Priority Queue
In computer science, a priority queue is an abstract data type which is like a regular queue or stack data structure, but where additionally each element has a "priority" associated with it. In a priority queue, an element with high priority is served before an element with low priority. If two elements have the same priority, they are served according to their order in the queue.
```
function PriorityQueue(){
    var items = [];
    function QueueElement (element, priority){
        this.element = element;
        this.priority = priority;
    }
    this.enqueue = function(element, priority){
        var queueElement = new QueueElement(element, priority);
        
        if(this.isEmpty()){
           items.push(queueElement); 
        }else{
            var added = false;
            for (var i=0; i< items.length; i++){
                if(queueElement.priority < items[i].priority){
                    items.splice(i, 0, queueElement);
                    added = true;
                    break;
                }
            }
            if(!added){
                items.push(queueElement);
            }
        }
    }
    //other methods - same as default Queue implementation
    this.dequeue = function () {
        return items.shift();
    }
    this.front = function () {
        return items[0];
    }
    this.isEmpty = function () {
        return items.length == 0;
    }
    this.size = function () {
        return items.length;
    }
    this.print = function () {
        var a = [];
        items.forEach(function(ele){
             a.push("{" + ele.element + ", " + ele.priority+"}")
        })
        console.log(a.toString());
    }
    this.get = function () {
        return items;
    }
}

var priorityQueue = new PriorityQueue();
priorityQueue.enqueue("John", 2);
priorityQueue.enqueue("Jack", 1);
priorityQueue.enqueue("Camila", 1);
priorityQueue.enqueue("Peter", 7);
priorityQueue.print();
```
## The Circular Queue - Hot Potato
We also have another modified version of the queue implementation, which is the circular queue. An example of a circular queue is the Hot Potato game. In this game, children are organized in a circle, and they pass the hot potato to their neighbor as fast as they can. At a certain point of the game, the hot potato stops being passed around the circle of children, and the child that has the hot potato is removed from the circle. This action is repeated until there is only one child left (the winner).
```
function hotPotato (nameList, num){
    var queue = new Queue();
    
    for (var i = 0; i < nameList.length; i++){
        queue.enqueue(nameList[i]);
    }
    
    var eliminated = '';
    while (queue.size() > 1){
        for (var i = 0; i < num; i++){
            queue.enqueue(queue.dequeue());
        }
        eliminated = queue.dequeue();
        console.log(eliminated + ' was elemited from the Hot Potato game.')
    }
    return queue.dequeue();
}

var names = ['John', 'Jack', 'Camila', 'Ingrid', 'Carl'];
var winner = hotPotato(names, 7);
console.log('The winner is: ' + winner);
```
