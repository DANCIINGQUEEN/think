## 1. Model : 스키마 정의
```js
const mongoose = require('mongoose')

const ticketSchema = new mongoose.Schema({
  movieName : String,
  price : Number,
  quantity : Number
})
module.exports = mongoose.model('Ticket', ticketSchema)
```

## 2. Service : 비즈니스 로직 처리
```js
const Ticket = require('../models/Ticket')
const getAllTickets = async () => {
  return await Ticket.find({})
}

const getTicketById = async (id) => {
  return await Ticket.findById(id)
}

const saveTicket = async (ticketData) => {
  const ticket = new Ticket(ticketData)
  return await ticket.save()
}

module.exports = {
  getAllTickets,
  getTicketById,
  saveTicket
}
```


## 3. Controller : HTTP 요청 처리
```js
const ticketService = require('../services/ticketService')

const getAllTickets = async (req, res) => {
  const tickets = await ticketService.getAllTickets()
  res.json(tickets)
}

const getTicketById = async (req, res) => {
  const ticket = await ticketService.getTicketById(req.params.id)
  res.json(ticket)
}

const saveTicket = asuync (req, res) => {
  const savedTicket = await ticketService.saveTicket(req.body)
  res.json(savedTicket)
}
module.exports = {
    getAllTickets,
    getTicketById,
    saveTicket
};
```


## 4. Routes : 라우트 설정
```js
const express = require('express');
const router = express.Router();
const ticketController = require('../controllers/ticketController');

router.get('/', ticketController.getAllTickets);
router.get('/:id', ticketController.getTicketById);
router.post('/', ticketController.saveTicket);

module.exports = router;
```


## 5. Express 애플리케이션 설정
```js
const express = require('express');
const mongoose = require('mongoose');
const ticketRoutes = require('./routes/tickets');
const app = express();

app.use(express.json());
app.use('/tickets', ticketRoutes);

mongoose.connect('mongodb://localhost/ticketdb', {
    useNewUrlParser: true,
    useUnifiedTopology: true
});

const port = 3000;
app.listen(port, () => {
    console.log(`Server is running on port ${port}`);
});

```
