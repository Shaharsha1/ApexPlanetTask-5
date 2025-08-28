# ApexPlanetTask-5
Objective:  Build a comprehensive web app and ensure its performance, responsiveness, and compatibility.  


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lumiere - Movie Ticket Booking</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #f5f5f5;
            color: #864daa;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        header {
            background-color: #0f0f1a;
            color: white;
            padding: 15px 0;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }

        .header-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 28px;
            font-weight: bold;
            color: #ff6b6b;
        }

        .logo span {
            color: white;
        }

        nav ul {
            display: flex;
            list-style: none;
        }

        nav ul li {
            margin-left: 25px;
        }

        nav ul li a {
            color: white;
            text-decoration: none;
            font-weight: 500;
            transition: color 0.3s;
        }

        nav ul li a:hover {
            color: #ff6b6b;
        }

        .hero {
            background: linear-gradient(rgba(0, 0, 0, 0.7), rgba(0, 0, 0, 0.7)), url('https://via.placeholder.com/1920x600') no-repeat center center/cover;
            height: 400px;
            display: flex;
            align-items: center;
            color: white;
            text-align: center;
        }

        .hero-content {
            width: 100%;
        }

        .hero h1 {
            font-size: 48px;
            margin-bottom: 20px;
        }

        .hero p {
            font-size: 20px;
            margin-bottom: 30px;
        }

        .btn {
            display: inline-block;
            background-color: #ff6b6b;
            color: white;
            padding: 12px 30px;
            border-radius: 30px;
            text-decoration: none;
            font-weight: bold;
            transition: all 0.3s;
            border: none;
            cursor: pointer;
        }

        .btn:hover {
            background-color: #ff5252;
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
        }

        .movies {
            padding: 60px 0;
        }

        .section-title {
            text-align: center;
            margin-bottom: 40px;
            font-size: 32px;
            color: #0f0f1a;
        }

        .movie-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 30px;
        }

        .movie-card {
            background-color: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s;
        }

        .movie-card:hover {
            transform: translateY(-10px);
        }

        .movie-poster {
            height: 350px;
            background-size: cover;
            background-position: center;
        }

        .movie-info {
            padding: 20px;
        }

        .movie-title {
            font-size: 20px;
            margin-bottom: 10px;
        }

        .movie-meta {
            display: flex;
            justify-content: space-between;
            color: #666;
            margin-bottom: 15px;
            font-size: 14px;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            z-index: 1000;
            overflow-y: auto;
        }

        .modal-content {
            background-color: white;
            margin: 50px auto;
            width: 80%;
            max-width: 800px;
            border-radius: 10px;
            overflow: hidden;
            animation: modalOpen 0.5s;
        }

        @keyframes modalOpen {
            from { opacity: 0; transform: translateY(-50px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .modal-header {
            padding: 20px;
            background-color: #0f0f1a;
            color: white;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .close-btn {
            background: none;
            border: none;
            color: white;
            font-size: 24px;
            cursor: pointer;
        }

        .modal-body {
            padding: 30px;
            display: flex;
            flex-direction: column;
        }

        .booking-steps {
            display: flex;
            justify-content: space-between;
            margin-bottom: 30px;
        }

        .step {
            text-align: center;
            flex: 1;
            position: relative;
        }

        .step-number {
            width: 40px;
            height: 40px;
            background-color: #ddd;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 0 auto 10px;
            font-weight: bold;
        }

        .step.active .step-number {
            background-color: #ff6b6b;
            color: white;
        }

        .step::after {
            content: '';
            position: absolute;
            top: 20px;
            left: 60%;
            width: 80%;
            height: 2px;
            background-color: #ddd;
            z-index: -1;
        }

        .step:last-child::after {
            display: none;
        }

        .step.active::after {
            background-color: #ff6b6b;
        }

        .step-title {
            font-size: 14px;
            color: #666;
        }

        .step.active .step-title {
            color: #0f0f1a;
            font-weight: bold;
        }

        .booking-form {
            display: none;
        }

        .booking-form.active {
            display: block;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
        }

        .form-control {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
        }

        .time-slots {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
            gap: 10px;
            margin-top: 10px;
        }

        .time-slot {
            padding: 10px;
            background-color: #f5f5f5;
            border-radius: 5px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
        }

        .time-slot:hover {
            background-color: #ddd;
        }

        .time-slot.selected {
            background-color: #ff6b6b;
            color: white;
        }

        .seats-container {
            margin-top: 20px;
        }

        .screen {
            text-align: center;
            margin-bottom: 30px;
            padding: 10px;
            background-color: #0f0f1a;
            color: white;
            font-weight: bold;
        }

        .seats-grid {
            display: grid;
            grid-template-columns: repeat(10, 1fr);
            gap: 10px;
            margin-bottom: 20px;
        }

        .seat {
            width: 30px;
            height: 30px;
            background-color: #ddd;
            border-radius: 5px;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            transition: all 0.3s;
        }

        .seat:hover {
            background-color: #ccc;
        }

        .seat.selected {
            background-color: #ff6b6b;
            color: white;
        }

        .seat.occupied {
            background-color: #aaa;
            cursor: not-allowed;
        }

        .seat-legend {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-bottom: 30px;
        }

        .legend-item {
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .legend-color {
            width: 20px;
            height: 20px;
            border-radius: 3px;
        }

        .booking-summary {
            background-color: #f9f9f9;
            padding: 20px;
            border-radius: 5px;
            margin-top: 20px;
        }

        .summary-item {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
        }

        .summary-total {
            font-weight: bold;
            font-size: 18px;
            border-top: 1px solid #ddd;
            padding-top: 10px;
            margin-top: 10px;
        }

        .form-actions {
            display: flex;
            justify-content: space-between;
            margin-top: 30px;
        }

        .btn-outline {
            background-color: transparent;
            border: 1px solid #0f0f1a;
            color: #0f0f1a;
        }

        .btn-outline:hover {
            background-color: #f5f5f5;
        }

        footer {
            background-color: #0f0f1a;
            color: white;
            padding: 40px 0;
        }

        .footer-content {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 30px;
            margin-bottom: 30px;
        }

        .footer-column h3 {
            color: #ff6b6b;
            margin-bottom: 20px;
            font-size: 18px;
        }

        .footer-column ul {
            list-style: none;
        }

        .footer-column ul li {
            margin-bottom: 10px;
        }

        .footer-column ul li a {
            color: #ddd;
            text-decoration: none;
            transition: color 0.3s;
        }

        .footer-column ul li a:hover {
            color: #ff6b6b;
        }

        .social-links {
            display: flex;
            gap: 15px;
        }

        .social-links a {
            color: white;
            font-size: 20px;
        }

        .copyright {
            text-align: center;
            padding-top: 20px;
            border-top: 1px solid #333;
            color: #aaa;
            font-size: 14px;
        }
    </style>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
</head>
<body>
    <header>
        <div class="container header-container">
            <div class="logo">Lumiere</div>
            <nav>
                <ul>
                    <li><a href="#">Home</a></li>
                    <li><a href="#">Movies</a></li>
                    <li><a href="#">Cinemas</a></li>
                    <li><a href="#">Offers</a></li>
                    <li><a href="#">Contact</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <section class="hero">
        <div class="container hero-content">
            <h1>Book Your Movie Tickets Online</h1>
            <p>Skip the line and reserve your seats in advance</p>
            <a href="#movies" class="btn">Browse Movies</a>
        </div>
    </section>

    <section class="movies" id="movies">
        <div class="container">
            <h2 class="section-title">Now Showing</h2>
            <div class="movie-grid">
                <div class="movie-card">
                    <div class="movie-poster" style="background-image: url('https://imgix.bustle.com/uploads/image/2020/4/20/5c2761e9-ad81-416d-8377-69cccf7ac274-endgame-1-fixx-22-xtra-logo-mine.jpg?w=374&h=551&fit=crop&crop=faces&dpr=2');"></div>
                    <div class="movie-info">
                        <h3 class="movie-title">Avengers: Endgame</h3>
                        <div class="movie-meta">
                            <span>PG-13</span>
                            <span>3h 1m</span>
                        </div>
                        <button class="btn book-btn" data-movie="Avengers: Endgame">Book Now</button>
                    </div>
                </div>

                <div class="movie-card">
                    <div class="movie-poster" style="background-image: url('https://mir-s3-cdn-cf.behance.net/project_modules/1400/78e3b466891157.5b26a37ceebf0.jpg');"></div>
                    <div class="movie-info">
                        <h3 class="movie-title">The Nun</h3>
                        <div class="movie-meta">
                            <span>PG-13</span>
                            <span>1h 36m</span>
                        </div>
                        <button class="btn book-btn" data-movie="The Nun">Book Now</button>
                    </div>
                </div>

                <div class="movie-card">
                    <div class="movie-poster" style="background-image: url('https://images-cdn.ubuy.co.in/634eec895d77b6101f502273-poster-stop-online-it-chapter-two.jpg');"></div>
                    <div class="movie-info">
                        <h3 class="movie-title">IT</h3>
                        <div class="movie-meta">
                            <span>PG-13</span>
                            <span>3h 12m</span>
                        </div>
                        <button class="btn book-btn" data-movie="IT">Book Now</button>
                    </div>
                </div>

                <div class="movie-card">
                    <div class="movie-poster" style="background-image: url('https://i.redd.it/mwzsmxngft531.jpg');"></div>
                    <div class="movie-info">
                        <h3 class="movie-title">Annabelle Comes Home</h3>
                        <div class="movie-meta">
                            <span>PG-13</span>
                            <span>1h 46m</span>
                        </div>
                        <button class="btn book-btn" data-movie="Annabelle Comes Home">Book Now</button>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <div class="modal" id="bookingModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Book Tickets</h2>
                <button class="close-btn">&times;</button>
            </div>
            <div class="modal-body">
                <div class="booking-steps">
                    <div class="step active" data-step="1">
                        <div class="step-number">1</div>
                        <div class="step-title">Select Time</div>
                    </div>
                    <div class="step" data-step="2">
                        <div class="step-number">2</div>
                        <div class="step-title">Choose Seats</div>
                    </div>
                    <div class="step" data-step="3">
                        <div class="step-number">3</div>
                        <div class="step-title">Confirm</div>
                    </div>
                </div>

                <div class="booking-form active" id="step1">
                    <h3 id="selectedMovie">Movie: Avengers: Endgame</h3>
                    <div class="form-group">
                        <label for="cinema">Select Cinema:</label>
                        <select id="cinema" class="form-control">
                            <option value="">-- Select Cinema --</option>
                            <option value="cineplex-downtown">Cineplex Downtown</option>
                            <option value="cineplex-midtown">Cineplex Midtown</option>
                            <option value="cineplex-uptown">Cineplex Uptown</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label for="date">Select Date:</label>
                        <input type="date" id="date" class="form-control">
                    </div>
                    <div class="form-group">
                        <label>Select Time:</label>
                        <div class="time-slots">
                            <div class="time-slot">10:00 AM</div>
                            <div class="time-slot">1:30 PM</div>
                            <div class="time-slot">4:45 PM</div>
                            <div class="time-slot">8:00 PM</div>
                            <div class="time-slot">10:30 PM</div>
                        </div>
                    </div>
                    <div class="form-actions">
                        <button class="btn btn-outline close-btn">Cancel</button>
                        <button class="btn next-step" data-next="2">Next</button>
                    </div>
                </div>

                <div class="booking-form" id="step2">
                    <h3>Choose Your Seats</h3>
                    <div class="seats-container">
                        <div class="screen">SCREEN</div>
                        <div class="seats-grid" id="seatsGrid">
                            <!-- Seats will be generated by JavaScript -->
                        </div>
                        <div class="seat-legend">
                            <div class="legend-item">
                                <div class="legend-color" style="background-color: #ddd;"></div>
                                <span>Available</span>
                            </div>
                            <div class="legend-item">
                                <div class="legend-color" style="background-color: #ff6b6b;"></div>
                                <span>Selected</span>
                            </div>
                            <div class="legend-item">
                                <div class="legend-color" style="background-color: #aaa;"></div>
                                <span>Occupied</span>
                            </div>
                        </div>
                    </div>
                    <div class="booking-summary">
                        <div class="summary-item">
                            <span>Seats:</span>
                            <span id="selectedSeatsText">None selected</span>
                        </div>
                        <div class="summary-item">
                            <span>Price per seat:</span>
                            <span>$12.00</span>
                        </div>
                        <div class="summary-item summary-total">
                            <span>Total:</span>
                            <span id="totalPrice">$0.00</span>
                        </div>
                    </div>
                    <div class="form-actions">
                        <button class="btn btn-outline prev-step" data-prev="1">Back</button>
                        <button class="btn next-step" data-next="3">Next</button>
                    </div>
                </div>

                <div class="booking-form" id="step3">
                    <h3>Confirm Your Booking</h3>
                    <div class="booking-summary">
                        <div class="summary-item">
                            <span>Movie:</span>
                            <span id="confirmMovie">Avengers: Endgame</span>
                        </div>
                        <div class="summary-item">
                            <span>Cinema:</span>
                            <span id="confirmCinema">Cineplex Downtown</span>
                        </div>
                        <div class="summary-item">
                            <span>Date & Time:</span>
                            <span id="confirmDateTime">May 15, 2023 at 8:00 PM</span>
                        </div>
                        <div class="summary-item">
                            <span>Seats:</span>
                            <span id="confirmSeats">A3, A4</span>
                        </div>
                        <div class="summary-item summary-total">
                            <span>Total:</span>
                            <span id="confirmTotal">$24.00</span>
                        </div>
                    </div>
                    <div class="form-group">
                        <label for="name">Full Name:</label>
                        <input type="text" id="name" class="form-control" placeholder="Enter your full name">
                    </div>
                    <div class="form-group">
                        <label for="email">Email:</label>
                        <input type="email" id="email" class="form-control" placeholder="Enter your email">
                    </div>
                    <div class="form-group">
                        <label for="phone">Phone Number:</label>
                        <input type="tel" id="phone" class="form-control" placeholder="Enter your phone number">
                    </div>
                    <div class="form-actions">
                        <button class="btn btn-outline prev-step" data-prev="2">Back</button>
                        <button class="btn" id="confirmBooking">Confirm Booking</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <footer>
        <div class="container">
            <div class="footer-content">
                <div class="footer-column">
                    <h3>About Lumiere</h3>
                    <p>Your premier destination for online movie ticket booking. Skip the queues and enjoy the show!</p>
                </div>
                <div class="footer-column">
                    <h3>Quick Links</h3>
                    <ul>
                        <li><a href="#">Home</a></li>
                        <li><a href="#">Movies</a></li>
                        <li><a href="#">Cinemas</a></li>
                        <li><a href="#">Offers</a></li>
                    </ul>
                </div>
                <div class="footer-column">
                    <h3>Help</h3>
                    <ul>
                        <li><a href="#">FAQs</a></li>
                        <li><a href="#">Contact Us</a></li>
                        <li><a href="#">Terms & Conditions</a></li>
                        <li><a href="#">Privacy Policy</a></li>
                    </ul>
                </div>
                <div class="footer-column">
                    <h3>Connect With Us</h3>
                    <div class="social-links">
                        <a href="#"><i class="fab fa-facebook-f"></i></a>
                        <a href="#"><i class="fab fa-twitter"></i></a>
                        <a href="#"><i class="fab fa-instagram"></i></a>
                        <a href="#"><i class="fab fa-youtube"></i></a>
                    </div>
                </div>
            </div>
            <div class="copyright">
                <p>&copy; 2023 Lumiere. All rights reserved.</p>
            </div>
        </div>
    </footer>

    <script>
      
        const modal = document.getElementById('bookingModal');
        const bookBtns = document.querySelectorAll('.book-btn');
        const closeBtns = document.querySelectorAll('.close-btn');
        const steps = document.querySelectorAll('.step');
        const bookingForms = document.querySelectorAll('.booking-form');
        const nextStepBtns = document.querySelectorAll('.next-step');
        const prevStepBtns = document.querySelectorAll('.prev-step');
        const timeSlots = document.querySelectorAll('.time-slot');
        const seatsGrid = document.getElementById('seatsGrid');
        const confirmBookingBtn = document.getElementById('confirmBooking');
        
  
        let bookingData = {
            movie: '',
            cinema: '',
            date: '',
            time: '',
            seats: [],
            pricePerSeat: 12,
            totalPrice: 0,
            name: '',
            email: '',
            phone: ''
        };

        
        function init() {
        
            generateSeats();
            
            
            bookBtns.forEach(btn => {
                btn.addEventListener('click', openBookingModal);
            });
            
            closeBtns.forEach(btn => {
                btn.addEventListener('click', closeModal);
            });
            
            timeSlots.forEach(slot => {
                slot.addEventListener('click', selectTimeSlot);
            });
            
            nextStepBtns.forEach(btn => {
                btn.addEventListener('click', goToNextStep);
            });
            
            prevStepBtns.forEach(btn => {
                btn.addEventListener('click', goToPrevStep);
            });
            
            confirmBookingBtn.addEventListener('click', confirmBooking);
            
          
            window.addEventListener('click', (e) => {
                if (e.target === modal) {
                    closeModal();
                }
            });
        }

      
        function openBookingModal(e) {
            const movieTitle = e.target.getAttribute('data-movie');
            bookingData.movie = movieTitle;
            document.getElementById('selectedMovie').textContent = `Movie: ${movieTitle}`;
            document.getElementById('confirmMovie').textContent = movieTitle;
            modal.style.display = 'block';
            document.body.style.overflow = 'hidden';
        }

      
        function closeModal() {
            modal.style.display = 'none';
            document.body.style.overflow = 'auto';
            resetBookingData();
        }

        function generateSeats() {
            const rows = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H'];
            let seatsHTML = '';
            
            rows.forEach(row => {
                for (let i = 1; i <= 10; i++) {
                    
                    const isOccupied = Math.random() < 0.3;
                    seatsHTML += `
                        <div class="seat ${isOccupied ? 'occupied' : ''}" data-row="${row}" data-number="${i}">
                            ${row}${i}
                        </div>
                    `;
                }
            });
            
            seatsGrid.innerHTML = seatsHTML;
            
        
            document.querySelectorAll('.seat:not(.occupied)').forEach(seat => {
                seat.addEventListener('click', selectSeat);
            });
        }


        function selectTimeSlot(e) {
            timeSlots.forEach(slot => slot.classList.remove('selected'));
            e.target.classList.add('selected');
            bookingData.time = e.target.textContent;
            
            
            const date = new Date(document.getElementById('date').value);
            const options = { year: 'numeric', month: 'long', day: 'numeric' };
            const formattedDate = date.toLocaleDateString('en-US', options);
            document.getElementById('confirmDateTime').textContent = 
                `${formattedDate} at ${bookingData.time}`;
        }

      
        function selectSeat(e) {
            e.target.classList.toggle('selected');
            const row = e.target.getAttribute('data-row');
            const number = e.target.getAttribute('data-number');
            const seatId = `${row}${number}`;
            
            if (e.target.classList.contains('selected')) {
                if (!bookingData.seats.includes(seatId)) {
                    bookingData.seats.push(seatId);
                }
            } else {
                bookingData.seats = bookingData.seats.filter(seat => seat !== seatId);
            }
            
            updateSeatsSummary();
        }

      
        function updateSeatsSummary() {
            const seatsText = bookingData.seats.length > 0 ? 
                bookingData.seats.join(', ') : 'None selected';
            document.getElementById('selectedSeatsText').textContent = seatsText;
            document.getElementById('confirmSeats').textContent = seatsText;
            
            bookingData.totalPrice = bookingData.seats.length * bookingData.pricePerSeat;
            document.getElementById('totalPrice').textContent = `$${bookingData.totalPrice.toFixed(2)}`;
            document.getElementById('confirmTotal').textContent = `$${bookingData.totalPrice.toFixed(2)}`;
        }

  
        function goToNextStep(e) {
            const nextStep = e.target.getAttribute('data-next');
            const currentStep = document.querySelector('.booking-form.active').id.replace('step', '');
            
    
            if (currentStep === '1') {
                if (!validateStep1()) {
                    return false;
                }
            
                bookingData.cinema = document.getElementById('cinema').value;
                bookingData.date = document.getElementById('date').value;
                document.getElementById('confirmCinema').textContent = 
                    document.getElementById('cinema').options[document.getElementById('cinema').selectedIndex].text;
            } else if (currentStep === '2') {
                if (!validateStep2()) {
                    return false;
                }
            }
            
        
            document.getElementById(`step${currentStep}`).classList.remove('active');
            document.getElementById(`step${nextStep}`).classList.add('active');
            
            
            steps.forEach(step => step.classList.remove('active'));
            document.querySelector(`.step[data-step="${nextStep}"]`).classList.add('active');
        }

  
        function goToPrevStep(e) {
            const prevStep = e.target.getAttribute('data-prev');
            const currentStep = document.querySelector('.booking-form.active').id.replace('step', '');
            
            document.getElementById(`step${currentStep}`).classList.remove('active');
            document.getElementById(`step${prevStep}`).classList.add('active');
            
            steps.forEach(step => step.classList.remove('active'));
            document.querySelector(`.step[data-step="${prevStep}"]`).classList.add('active');
        }

    
        function validateStep1() {
            const cinemaSelect = document.getElementById('cinema');
            const dateInput = document.getElementById('date');
            const selectedTimeSlot = document.querySelector('.time-slot.selected');
            
            if (!cinemaSelect.value) {
                alert('Please select a cinema');
                return false;
            }
            
            if (!dateInput.value) {
                alert('Please select a date');
                return false;
            }
            
            if (!selectedTimeSlot) {
                alert('Please select a time slot');
                return false;
            }
            
            return true;
        }

      
        function validateStep2() {
            if (bookingData.seats.length === 0) {
                alert('Please select at least one seat');
                return false;
            }
            
            return true;
        }

        
        function confirmBooking() {
            bookingData.name = document.getElementById('name').value;
            bookingData.email = document.getElementById('email').value;
            bookingData.phone = document.getElementById('phone').value;
            
            if (!bookingData.name || !bookingData.email || !bookingData.phone) {
                alert('Please fill in all your contact details');
                return;
            }
            
            
            console.log('Booking confirmed:', bookingData);
            alert(`Booking confirmed!\n\nMovie: ${bookingData.movie}\nSeats: ${bookingData.seats.join(', ')}\nTotal: $${bookingData.totalPrice.toFixed(2)}`);
            
            closeModal();
        }


        function resetBookingData() {
            bookingData = {
                movie: '',
                cinema: '',
                date: '',
                time: '',
                seats: [],
                pricePerSeat: 12,
                totalPrice: 0,
                name: '',
                email: '',
                phone: ''
            };
            
          
            document.getElementById('cinema').selectedIndex = 0;
            document.getElementById('date').value = '';
            timeSlots.forEach(slot => slot.classList.remove('selected'));
            document.querySelectorAll('.seat.selected').forEach(seat => seat.classList.remove('selected'));
            document.getElementById('selectedSeatsText').textContent = 'None selected';
            document.getElementById('totalPrice').textContent = '$0.00';
            document.getElementById('name').value = '';
            document.getElementById('email').value = '';
            document.getElementById('phone').value = '';
            
        
            bookingForms.forEach(form => form.classList.remove('active'));
            document.getElementById('step1').classList.add('active');
            steps.forEach(step => step.classList.remove('active'));
            document.querySelector('.step[data-step="1"]').classList.add('active');
        }

        
        document.addEventListener('DOMContentLoaded', init);
    </script>
</body>
</html>
