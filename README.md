<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>movie seat booking</title>
    <link rel="stylesheet" href="movie-seat.css">
</head>
<body>
    <div class="movie-container">
        <label for="movie">Pick a movie</label>
        <select name="movie" id ="movie">
            <option value="10"> Salakaar (10$)</option>
            <option value="8"> War 2 (8$)</option>
            <option value="9"> Saiyaara (9$)</option>
            <option value="10"> Special Ops 2.0 (10$)</option>
        </select>
    </div>

        <ul class="showcase">
            <li>
                <div class="seat"></div>
                    <small>N/A</small>
            </li>
            <li>
                <div class="seat Selected"></div>
                <small>Selected</small>
            </li>
            <li>
                <div class="seat Occupied"></div>
                <small>Occupied</small>
            </li>
        </ul>

        <div class="container">
            <div class="screen"></div>
            <div class="row">
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat Occupied"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
            </div>

             <div class="row">
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat Occupied"></div>
                <div class="seat Occupied"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
            </div>

             <div class="row">
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
            </div>

             <div class="row">
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
            </div>

             <div class="row">
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
            </div>

             <div class="row">
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
            </div>

             <div class="row">
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat Occupied"></div>
                <div class="seat Occupied"></div>
                <div class="seat Occupied"></div>
                <div class="seat"></div>
                <div class="seat"></div>
            </div>

             <div class="row">
                <div class="seat Occupied"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat"></div>
                <div class="seat Occupied"></div>
                <div class="seat"></div>
            </div>
        </div>

        <p class="text">You have selected<span id="count"> 0 </span>seats for a price of $<span id="total"> 0 </span></p>

        <script src="movie-seat.js"></script>
</body>
</html>
const container =document.querySelector(".container");
const seats = document.querySelectorAll(".row .seat:not(.Occupied)");
const count = document.getElementById("count")
const total =document.getElementById("total")
const movieSelect = document.getElementById("movie")
let ticketPrice = +movieSelect.value;

function populateUI(){
    const selectedSeats =JSON.parse(localStorage.getItem("selectedSeats"));
    if(selectedSeats !== null && selectedSeats.length>0){
        seats.forEach((seat,index)=>{
            if(selectedSeats.indexOf(index)> -1) seat.classList.add("Selected");
        });
    }

    const selectedMovieIndex = localStorage.getItem("selectedMovieIndex");
    if(selectedMovieIndex !== null)
        movieSelect.selectedIndex = selectedMovieIndex;
}

function setMovieData(movieIndex, moviePrice){
    localStorage.setItem("selectedMovieIndex",movieIndex)
    localStorage.setItem("selectedMoviePrice",moviePrice)
}

function updateSelectedCount(){
    const selectedSeats = document.querySelectorAll(".row .seat.Selected")
    const seatsIndex =[...selectedSeats].map((seat)=> [...seats].indexOf(seat))

    localStorage.setItem("selectedSeats",JSON.stringyfy(seatsIndex))
    const selectedSeatsCount = selectedSeats.length;
    count.innerText = selectedSeatsCount;
    total.innerText = selectedSeatsCount * ticketPrice;
}

movieSelect.addEventListener("change",(e)=>{
    ticketPrice = +e.target.value;
    setMovieData(e.target.selectedIndex,e.target.value);
    updateSelectedCount();
});

container.addEventListener("click",(e)=>{
     if(
        e.target.classList.contains("seat")&& !e.target.classList.contains("Occupied")){
            e.target.classList.toggle("Selected");
            updateSelectedCount();
        }
     })

populateUI();
updateSelectedCount();
*{
    margin: 0%;
    padding: 0%;
    box-sizing: border-box;
}

body{
    background-color: #2a2929;
    color: white;
    font-family: sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    margin: 0;
}
.movie-container{
    margin: 20px 0;
}
.movie-container select{
    background-color: #fff;
    border: 0;
    border-radius: 5px;
    font-size: 14px;
    font-family: inherit;
    margin-left: 10px;
    padding: 5px 15px;
    -moz-appearance: none;
    -webkit-appearance: none;
    appearance: none;
}
.container{
    perspective:1000px;
    margin-bottom:30px;
}
.seat{
    background-color: #0c0c0c;
    height:12px;
    width:15px;
    margin: 3px;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
}
.seat.Selected{
    background-color: aqua;
}
.seat.Occupied{
    background-color: #eb5b5b;
}
.seat:nth-of-type(2){
    margin-right: 18px;
}
.seat:nth-last-of-type(2){
    margin-left: 18px;
}
.seat:not(.seat-Occupied):hover{
    cursor: pointer;
    transform: scale(1.2);
}
.showcase .seat:not(.seat-Occupied):hover{
    cursor: default;
    transform: scale(1);

}
.showcase{
    background: rgba(0,0,0,0.1);
    padding: 5px 10px;
    border-radius: 5px;
    color:#777;
    list-style-type: none;
    display: flex;
    justify-content: space-between;
}
.showcase li{
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 10px;
}
.showcase li{
    margin-left: 2px;
}
.showcase li small{
    margin-left: 2px;
}
.row{
    display: flex;
}
.screen{
    background-color: #fff;
    height: 70px;
    width: 100%;
    margin:15px 0;
    transform: rotateX(-45deg);
    box-shadow: 0 3px 10px rgba(255,255,255,0.7);
}
p.text{
    margin: 5px 0;
}
p.text span{
    color:rgb(164, 251, 222)
}
