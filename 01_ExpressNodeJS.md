# Advanced Full Stack
# Express (node.js)
## Backend
- Data afhandelen
- Security
- Communicatie
+ Schaalbaarheid
+ Framework
+ Flexibiliteit

## Node.js
An asynchronous event-driven JavaScript runtime.
Designed to build scalable network applications.

- Event driven
- Gelijkaardige structuur zoals in de browser
- Afhankelijk van de event loop
- basis voor snel én veel
- Ideaal voor backend
  - HTTP request => event => callback
  - GET, DELETE, PUT, OPTIONS, etc...

### Don'ts
- Computing / heavy lifting
- Alle zware processing taken of threading
- State bijhouden

### Let's get started
- Enkel node.js
- Beter: een framework

## Express
Fast, unopinionated, minimalist web framework for Node.js

Unopinionated: hele toolbox, maar zelf een hand in

- Helpt met structuur / eenvoud
- Niet te strikt

+ Eenvoudig

### Typescript
Enkel in onze dev-omgeving, omgezet naar gewone JS in production (build).

Nieuwste JS onderdelen gebruiken, deze wordt omgezet naar JS-code die goed ondersteund wordt.

### JSON
Met JSON werken in onze requests of responses.
```javascript
app.use(express.json)
```
Nu kan je request uit de body halen.
Nu kan je JSON sturen vanuit een response.
```javascript
res.json({ ... })
```

### Middleware
.use syntax is middleware bij express

- Geeft telkens iets door aan de rest die erna komt.
- Kan iets toevoegen aan de response of request.
- Enkel een tussenstap, gaat daarna verder
- Typisch logging & authentication
- Elke request doorloopt volgens de volgorde waar het staat in de file.

## Summary
1. **Wat is Node.JS**
2. **Wat is Express?**
3. **Wat is middleware?**
4. **Wat is event-driven?**
- Gelijkaardige structuur als in de browser. Driven by events, such as actions, sensor outputs, message passing from other programs... Actions in response to user input.
5. **Hoe werkt de event-loop?**
- Incoming requests komen in de event queue en worden één per één in de event loop afgehandeld door een worker.
- Elke HTTP request is een "event" waarop je een callback uitvoert.
  - *Bv. GET is een event, we voeren daar een callback voor uit.*
6. **Hoe schrijf je async JS-code?**
- Met behulp van async, await, (promises)...
7. **Wat is een typische Express structuur?**
```typescript
import express, { Request, Response } from 'express';

const app = express(),
  port = process.env.PORT || 3000;

// Dan luisteren we naar 'events'.
app.listen(port, () => {
  console.info(`\nServer 👾 \nListening on http://localhost:${port}/`);
});

// Routes
app.get('/', (req: Request, res: Response) => {
  res.send('Hello World!');
});
```