<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dashboard Financiero - Samuel</title>
    <style>
        :root {
            --primary-color: #121212;
            --secondary-color: #1e1e1e;
            --font-color: #e0e0e0;
            --accent-color: #007bff;
            --secondary-accent-color: #f5a623;
            --card-shadow: rgba(0, 0, 0, 0.4);
            --danger-color: #e74c3c;
            --success-color: #28a745;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background-color: var(--primary-color);
            color: var(--font-color);
            margin: 0;
            padding: 20px;
            line-height: 1.6;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        .welcome-header {
            text-align: center;
            margin-bottom: 20px;
        }
        .welcome-header h1 {
            font-size: 1.8em;
            font-weight: 300;
            margin-bottom: 5px;
        }
        .welcome-header #current-date {
            font-size: 1rem;
            font-weight: 400;
            color: #b0b0b0;
        }

        .main-summary-section {
            text-align: center;
            background-color: var(--secondary-color);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 15px;
        }
        .main-summary-section h2 {
            margin-top: 0;
            font-size: 1.2em;
            font-weight: 300;
            color: #b0b0b0;
        }
        
        .projection-section {
            text-align: center;
            background-color: var(--secondary-color);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 40px;
        }
        .projection-section h2 {
             margin-top: 0;
            font-size: 1.2em;
            font-weight: 300;
            color: #b0b0b0;
        }

        .payment-breakdown-total {
            font-size: 2.5em;
            font-weight: bold;
            color: var(--accent-color);
            margin: 0 0 15px 0;
        }
        .payment-breakdown-samuel {
            font-size: 1.8em;
            font-weight: bold;
            color: var(--font-color);
            margin: 0 0 15px 0;
        }
        .projection-section .payment-breakdown-total {
            font-size: 1.8em;
        }
        .projection-section .payment-breakdown-samuel {
            font-size: 1.5em;
        }
        .other-payments-title {
            font-size: 1em;
            color: #b0b0b0;
            margin-top: 15px;
            border-top: 1px solid #444;
            padding-top: 15px;
            font-weight: 500;
        }
        .other-payments p {
            font-size: 1.1em;
            margin: 5px 0;
            color: var(--font-color);
        }


        .cards-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .cards-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 25px;
            margin-bottom: 40px;
        }

        .card {
            background: var(--secondary-color);
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 8px 16px var(--card-shadow);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .card:hover {
            transform: translateY(-8px);
            box-shadow: 0 12px 24px var(--card-shadow);
        }
        
        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .card-name {
            font-size: 1.3em;
            font-weight: 600;
            outline: none;
        }
        
        .card-name:focus {
            border-bottom: 1px solid var(--accent-color);
        }

        .card-controls {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .card-limit, .card-dates {
            font-size: 0.95em;
            color: #b0b0b0;
        }
        
        .editable {
            outline: none;
            padding: 2px 4px;
            border-radius: 4px;
        }

        .editable:focus {
            background-color: rgba(255, 255, 255, 0.1);
        }

        .card-payment-due {
            font-size: 1.1em;
            font-weight: 500;
            color: var(--secondary-accent-color);
            margin-top: 10px;
            padding-top: 10px;
            border-top: 1px solid #333;
        }

        .card-summary {
            margin-top: auto;
            font-size: 1.8em;
            font-weight: bold;
            color: var(--accent-color);
            align-self: flex-end;
        }

        .new-expense-btn {
            position: fixed;
            bottom: 30px;
            right: 30px;
            background-color: var(--accent-color);
            color: white;
            border: none;
            border-radius: 50%;
            width: 60px;
            height: 60px;
            font-size: 30px;
            cursor: pointer;
            box-shadow: 0 4px 12px rgba(0, 123, 255, 0.4);
            transition: transform 0.2s ease;
            z-index: 1000;
        }

        .new-expense-btn:hover {
            transform: scale(1.1);
        }

        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.7);
            display: flex;
            justify-content: center;
            align-items: center;
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.3s ease, visibility 0.3s ease;
            z-index: 999;
        }

        .modal-overlay.active {
            opacity: 1;
            visibility: visible;
        }
        
        .modal-content {
            background: var(--secondary-color);
            padding: 30px;
            border-radius: 15px;
            width: 90%;
            max-width: 500px;
            transform: translateY(50px);
            transition: transform 0.4s ease;
            max-height: 85vh;
            overflow-y: auto;
        }

        .modal-overlay.active .modal-content {
            transform: translateY(0);
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
        }

        .form-group input, .form-group select {
            width: 100%;
            padding: 12px;
            border-radius: 8px;
            border: 1px solid #444;
            background-color: #333;
            color: var(--font-color);
            box-sizing: border-box;
        }
        
        #deferred-options {
            display: none;
            padding-left: 15px;
            border-left: 2px solid var(--accent-color);
        }

        .main-content-section {
            background-color: var(--secondary-color);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
        }
        
        .month-navigation {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        .month-navigation h3 {
            margin: 0;
            font-size: 1.5em;
            color: var(--secondary-accent-color);
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
        }
        
        th, td {
            padding: 15px;
            border-bottom: 1px solid #333;
            text-align: left;
        }

        th {
            font-weight: 600;
        }
        
        .color-picker {
            -webkit-appearance: none;
            -moz-appearance: none;
            appearance: none;
            width: 28px;
            height: 28px;
            background-color: transparent;
            border: none;
            cursor: pointer;
        }
        .color-picker::-webkit-color-swatch {
            border-radius: 50%;
            border: 2px solid #555;
        }

        .delete-card-btn {
            background: none;
            border: none;
            color: var(--danger-color);
            font-size: 1.2em;
            cursor: pointer;
            transition: color 0.2s;
        }
        .delete-card-btn:hover {
            color: #ff7668;
        }

        .btn {
            padding: 12px 20px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            transition: background-color 0.2s;
        }
        
        .btn-primary {
            background-color: var(--accent-color);
            color: white;
        }
        .btn-primary:hover {
            background-color: #0069d9;
        }

        .btn-secondary {
            background-color: #444;
            color: white;
            margin-right: 10px;
        }
        .btn-secondary:hover {
            background-color: #555;
        }

        .btn-action {
            background: var(--accent-color);
            color: white;
            border: none;
            padding: 5px 10px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 0.9em;
            margin-right: 5px;
        }
        .btn-action:disabled {
            background-color: #555;
            cursor: not-allowed;
        }

        .btn-delete-expense {
            background: var(--danger-color);
            color: white;
            border: none;
            padding: 5px 10px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 0.9em;
        }
        .btn-delete-expense:hover {
            background: #c0392b;
        }

        /* Styles for person summary */
        .summary-details {
            margin-bottom: 10px;
        }
        .summary-details summary {
            font-size: 1.2em;
            font-weight: 500;
            cursor: pointer;
        }
        .summary-details ul {
            list-style-type: none;
            padding-left: 20px;
            border-left: 2px solid var(--accent-color);
            margin-top: 10px;
        }
        .summary-details li {
            padding: 8px 0;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        #deferred-debt-container p {
            font-size: 1.2em;
            margin: 8px 0;
        }
        
        /* Styles for payment tracking */
        .payment-list {
            list-style-type: none;
            padding: 0;
        }
        .payment-list li {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            border-bottom: 1px solid #333;
        }
        .payment-list li.paid {
            text-decoration: line-through;
            color: #888;
        }
        .payment-summary {
            margin-top: 20px;
            padding-top: 20px;
            border-top: 1px solid #444;
            font-size: 1.2em;
        }

    </style>
</head>
<body>

    <div class="container">
        <div class="welcome-header">
            <h1>Bienvenido, Samuel</h1>
            <p id="current-date"></p>
        </div>

        <div class="main-summary-section">
            <h2 id="summary-title">Total a Pagar este Mes</h2>
            <div id="total-monthly-payment"></div>
        </div>

        <div class="projection-section">
            <div id="projection-result"></div>
        </div>
        
        <div class="cards-header">
            <h2>Tus Tarjetas</h2>
            <button class="btn btn-primary" onclick="addCard()">+ Agregar Tarjeta</button>
        </div>

        <div class="cards-container" id="cards-container">
            <!-- Las tarjetas de crédito se generarán aquí dinámicamente -->
        </div>
        
        <div class="main-content-section">
            <h2>Personas</h2>
            <div id="people-list" style="margin-bottom:15px;"></div>
            <input type="text" id="new-person-name" placeholder="Agregar nuevo nombre" style="padding: 10px; border-radius: 5px; border: 1px solid #444; background: #333; color: var(--font-color); margin-right: 10px;">
            <button class="btn btn-primary" onclick="addPerson()">Agregar</button>
        </div>

        <div class="main-content-section">
            <h2 id="person-summary-title">Resumen por Persona</h2>
            <div id="person-summary-container"></div>
        </div>

        <div class="main-content-section">
            <h2>Deuda Total en Pagos Diferidos</h2>
            <div id="deferred-debt-container"></div>
        </div>

        <div class="main-content-section">
            <h2>Pagos del Mes</h2>
            <div id="payment-tracker-container"></div>
        </div>

        <div class="main-content-section">
            <div class="month-navigation">
                <button class="btn btn-secondary" onclick="showPreviousMonth()">&lt; Mes Anterior</button>
                <h3 id="history-month-year"></h3>
                <button class="btn btn-secondary" onclick="showNextMonth()">Mes Siguiente &gt;</button>
            </div>
            <div id="expenses-table-container">
                <!-- El contenido de los gastos por mes se generará aquí -->
            </div>
            <div style="margin-top: 20px;">
                <button class="btn btn-secondary" onclick="exportToCSV()">Exportar a Excel (CSV)</button>
                <button class="btn btn-secondary" onclick="exportToText()">Exportar para Word (Texto)</button>
            </div>
        </div>
    </div>

    <button class="new-expense-btn" onclick="openExpenseForm()">+</button>

    <div class="modal-overlay" id="expense-form-overlay">
        <div class="modal-content" id="expense-form-content">
            <h2 id="modal-title" style="margin-top:0;">Nuevo Gasto</h2>
            <input type="hidden" id="editing-expense-id">
            <div class="form-group">
                <label for="expense-description">Descripción</label>
                <input type="text" id="expense-description" required>
            </div>
             <div class="form-group">
                <label for="expense-date">Mes de Registro</label>
                <select id="expense-date"></select>
            </div>
            <div class="form-group">
                <label for="expense-amount" id="amount-label">Monto Total</label>
                <input type="number" id="expense-amount" required>
            </div>
            <div class="form-group">
                <label for="expense-card">Tarjeta</label>
                <select id="expense-card"></select>
            </div>
            <div class="form-group">
                <label for="expense-person">Persona</label>
                <select id="expense-person"></select>
            </div>
            <div class="form-group">
                <label for="payment-type">Tipo de Pago</label>
                <select id="payment-type" onchange="toggleDeferredOptions()">
                    <option value="single">Pago Único</option>
                    <option value="deferred">Pago Diferido</option>
                </select>
            </div>
            <div id="deferred-options">
                <div class="form-group">
                    <label for="total-installments">Total de Meses</label>
                    <input type="number" id="total-installments" value="3" min="2">
                </div>
                <div class="form-group">
                    <label for="current-installment">Mes Actual (en el que vas)</label>
                    <input type="number" id="current-installment" value="1" min="1">
                </div>
            </div>
            <button id="modal-submit-button" class="btn btn-primary" onclick="processExpense()">Registrar Gasto</button>
        </div>
    </div>
    
    <script>
        // --- DATA MODEL & PERSISTENCE ---
        let cards = JSON.parse(localStorage.getItem('cards')) || [];
        let expenses = JSON.parse(localStorage.getItem('expenses')) || [];
        let people = JSON.parse(localStorage.getItem('people')) || ['Samuel'];
        let displayedDate = new Date();

        function saveData() {
            localStorage.setItem('cards', JSON.stringify(cards));
            localStorage.setItem('expenses', JSON.stringify(expenses));
            localStorage.setItem('people', JSON.stringify(people));
        }

        // --- RENDER FUNCTIONS ---
        function renderAll() {
            renderCards();
            renderPeople();
            renderSummaryByPerson();
            renderDeferredDebtByPerson();
            renderPaymentTracker();
            renderExpensesForDisplayedMonth();
            renderTotalMonthlyPayment();
            renderNextMonthProjection();
            updateMonthDisplay();
        }

        function displayCurrentDate() {
            const dateEl = document.getElementById('current-date');
            const now = new Date();
            const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            dateEl.innerText = now.toLocaleDateString('es-MX', options);
        }

        function renderCards() {
            const container = document.getElementById('cards-container');
            container.innerHTML = '';
            cards.forEach(card => {
                const totalDebt = calculateTotalDebt(card.id);
                const remainingBalance = card.limit - totalDebt;
                const paymentDue = calculateTotalDueForCard(card.id, displayedDate);
                const cardEl = document.createElement('div');
                cardEl.className = 'card';
                cardEl.style.borderTop = `5px solid ${card.color}`;
                cardEl.innerHTML = `
                    <div class="card-header">
                        <span class="card-name" contenteditable="true" onblur="updateCardDetail(${card.id}, 'name', this.innerText)">${card.name}</span>
                        <div class="card-controls">
                            <input type="color" class="color-picker" value="${card.color}" oninput="updateCardDetail(${card.id}, 'color', this.value)">
                            <button class="delete-card-btn" onclick="deleteCard(${card.id})">&times;</button>
                        </div>
                    </div>
                    <div class="card-limit">Límite: $<span class="editable" contenteditable="true" onblur="updateCardDetail(${card.id}, 'limit', this.innerText)">${card.limit}</span></div>
                    <div class="card-dates">
                        Corte: Día <span class="editable" contenteditable="true" onblur="updateCardDetail(${card.id}, 'cutDay', this.innerText)">${card.cutDay}</span> | 
                        Pago: Día <span class="editable" contenteditable="true" onblur="updateCardDetail(${card.id}, 'payDay', this.innerText)">${card.payDay}</span>
                    </div>
                    <div class="card-payment-due">
                        Pago del mes: <strong>$${paymentDue.toFixed(2)}</strong>
                    </div>
                    <div class="card-summary" title="Saldo restante">$${remainingBalance.toFixed(2)}</div>
                `;
                container.appendChild(cardEl);
            });
            updateCardOptionsInForm();
        }

        function renderPeople() {
            const list = document.getElementById('people-list');
            const select = document.getElementById('expense-person');
            list.innerHTML = people.map(p => `<span style="background:#333; padding: 5px 10px; border-radius: 15px; margin-right: 5px;">${p}</span>`).join('');
            select.innerHTML = people.map(p => `<option value="${p}">${p}</option>`).join('');
        }

        function renderSummaryByPerson() {
            const container = document.getElementById('person-summary-container');
            const title = document.getElementById('person-summary-title');
            title.innerHTML = `Resumen por Persona (${displayedDate.toLocaleString('es-MX', { month: 'long', year: 'numeric' })})`;
            container.innerHTML = '';

            people.forEach(person => {
                const monthStart = new Date(displayedDate.getFullYear(), displayedDate.getMonth(), 1);
                const monthEnd = new Date(displayedDate.getFullYear(), displayedDate.getMonth() + 1, 0);
                
                const personExpensesThisMonth = expenses.filter(exp => {
                    const expDate = new Date(exp.date);
                    return exp.person === person && expDate >= monthStart && expDate <= monthEnd;
                });

                if (personExpensesThisMonth.length === 0) return;

                const expensesByCard = personExpensesThisMonth.reduce((acc, exp) => {
                    const card = cards.find(c => c.id === exp.cardId);
                    const cardName = card ? card.name : 'Sin Tarjeta';
                    if (!acc[cardName]) acc[cardName] = [];
                    acc[cardName].push(exp);
                    return acc;
                }, {});

                const totalSpentThisMonth = personExpensesThisMonth.reduce((total, exp) => total + exp.amount, 0);

                const personDetails = document.createElement('details');
                personDetails.className = 'summary-details';
                personDetails.innerHTML = `<summary>${person}: <strong>$${totalSpentThisMonth.toFixed(2)}</strong> (Gastos del mes)</summary>`;
                
                Object.keys(expensesByCard).forEach(cardName => {
                    const cardDetails = document.createElement('details');
                    cardDetails.style.paddingLeft = '20px';
                    cardDetails.innerHTML = `<summary>${cardName}</summary>
                        <ul>
                            ${expensesByCard[cardName].map(exp => `<li>
                                <span>${new Date(exp.date).toLocaleDateString('es-MX')}: ${exp.description} - $${exp.amount.toFixed(2)}</span>
                                <div>
                                    <button class="btn-action" onclick="editExpense(${exp.id})">Editar</button>
                                    <button class="btn-delete-expense" onclick="deleteExpense(${exp.id})">Eliminar</button>
                                </div>
                            </li>`).join('')}
                        </ul>
                    `;
                    personDetails.appendChild(cardDetails);
                });
                container.appendChild(personDetails);
            });
        }

        function renderDeferredDebtByPerson() {
            const container = document.getElementById('deferred-debt-container');
            container.innerHTML = '';
            const debtByPerson = {};

            expenses.forEach(exp => {
                if (exp.type === 'deferred') {
                    const registrationDate = new Date(exp.date);
                    const firstInstallmentDate = new Date(registrationDate.getFullYear(), registrationDate.getMonth() - (exp.currentInstallment - 1), 1);
                    const now = new Date();
                    
                    if (now >= firstInstallmentDate) {
                        const monthsPassed = (now.getFullYear() - firstInstallmentDate.getFullYear()) * 12 + (now.getMonth() - firstInstallmentDate.getMonth());
                        const currentInstallmentNumber = monthsPassed + 1;

                        if (currentInstallmentNumber > 0 && currentInstallmentNumber <= exp.totalInstallments) {
                            const remainingInstallments = exp.totalInstallments - currentInstallmentNumber + 1;
                            const remainingDebt = exp.amount * remainingInstallments;

                            if (!debtByPerson[exp.person]) debtByPerson[exp.person] = 0;
                            debtByPerson[exp.person] += remainingDebt;
                        }
                    }
                }
            });

            if (Object.keys(debtByPerson).length > 0) {
                Object.keys(debtByPerson).forEach(person => {
                    const personEl = document.createElement('p');
                    personEl.innerHTML = `${person}: <strong>$${debtByPerson[person].toFixed(2)}</strong>`;
                    container.appendChild(personEl);
                });
            } else {
                container.innerHTML = '<p>No hay deudas por pagos diferidos activos.</p>';
            }
        }

        function renderPaymentTracker() {
            const container = document.getElementById('payment-tracker-container');
            const dueExpenses = getDueExpensesForDate(displayedDate);
            container.innerHTML = '';

            if (dueExpenses.length === 0) {
                container.innerHTML = '<p>No hay pagos para este mes.</p>';
                return;
            }

            const list = document.createElement('ul');
            list.className = 'payment-list';
            let totalPaid = 0;
            let totalDue = 0;

            dueExpenses.forEach(exp => {
                const li = document.createElement('li');
                if (exp.paid) {
                    li.className = 'paid';
                    totalPaid += exp.amount;
                }
                totalDue += exp.amount;
                
                li.innerHTML = `
                    <div>
                        <input type="checkbox" id="pay-${exp.id}" onchange="togglePaymentStatus(${exp.id})" ${exp.paid ? 'checked' : ''}>
                        <label for="pay-${exp.id}">${exp.description} (${exp.person})</label>
                    </div>
                    <span>$${exp.amount.toFixed(2)}</span>
                `;
                list.appendChild(li);
            });
            container.appendChild(list);

            const summary = document.createElement('div');
            summary.className = 'payment-summary';
            summary.innerHTML = `
                <p>Total del Mes: <strong>$${totalDue.toFixed(2)}</strong></p>
                <p style="color: var(--success-color);">Pagado: <strong>$${totalPaid.toFixed(2)}</strong></p>
                <p style="color: var(--danger-color);">Restante: <strong>$${(totalDue - totalPaid).toFixed(2)}</strong></p>
            `;
            container.appendChild(summary);
        }

        function renderExpensesForDisplayedMonth() {
            const contentContainer = document.getElementById('expenses-table-container');
            const now = new Date();
            const isFutureMonth = new Date(displayedDate.getFullYear(), displayedDate.getMonth(), 1) > new Date(now.getFullYear(), now.getMonth(), 1);

            let expensesToShow = [];
            if (isFutureMonth) {
                expensesToShow = getProjectedDeferredExpensesForDate(displayedDate);
            } else {
                const monthStart = new Date(displayedDate.getFullYear(), displayedDate.getMonth(), 1);
                const monthEnd = new Date(displayedDate.getFullYear(), displayedDate.getMonth() + 1, 0);
                expensesToShow = expenses.filter(exp => {
                    const expDate = new Date(exp.date);
                    return expDate >= monthStart && expDate <= monthEnd;
                });
            }

            let tableHTML = '<table><thead><tr><th>Descripción</th><th>Monto</th><th>Persona</th><th>Tarjeta</th><th>Tipo</th><th>Acciones</th></tr></thead><tbody>';
            if (expensesToShow.length > 0) {
                expensesToShow.forEach(exp => {
                    const card = cards.find(c => c.id === exp.cardId);
                    let paymentInfo = exp.type === 'single' ? 'Único' : `Diferido (${exp.currentInstallment}/${exp.totalInstallments})`;
                    let amountDisplay = exp.amount;
                    tableHTML += `<tr>
                        <td>${exp.description} ${exp.isProjection ? '(Proyectado)' : ''}</td>
                        <td>$${amountDisplay.toFixed(2)}</td>
                        <td>${exp.person}</td>
                        <td>${card ? card.name : 'N/A'}</td>
                        <td>${paymentInfo}</td>
                        <td>
                            <button class="btn-action" onclick="editExpense(${exp.id})" ${exp.isProjection ? 'disabled' : ''}>Editar</button>
                            <button class="btn-delete-expense" onclick="deleteExpense(${exp.id})">Eliminar</button>
                        </td>
                    </tr>`;
                });
            } else {
                tableHTML += `<tr><td colspan="6" style="text-align:center;">No hay movimientos ${isFutureMonth ? 'proyectados' : 'registrados'} para este mes.</td></tr>`;
            }
            tableHTML += '</tbody></table>';
            contentContainer.innerHTML = tableHTML;
        }
        
        function renderTotalMonthlyPayment() {
            const title = document.getElementById('summary-title');
            title.innerText = `Total a Pagar en ${displayedDate.toLocaleString('es-MX', { month: 'long' })}`;
            const breakdown = getPaymentBreakdownForDate(displayedDate, true); // Get only unpaid
            const container = document.getElementById('total-monthly-payment');
            container.innerHTML = '';

            const total = Object.values(breakdown).reduce((sum, val) => sum + val, 0);
            const totalEl = document.createElement('p');
            totalEl.className = 'payment-breakdown-total';
            totalEl.innerHTML = `Total Restante: <strong>$${total.toFixed(2)}</strong>`;
            container.appendChild(totalEl);

            const samuelTotal = breakdown['Samuel'] || 0;
            const samuelEl = document.createElement('p');
            samuelEl.className = 'payment-breakdown-samuel';
            samuelEl.innerHTML = `Samuel: <strong>$${samuelTotal.toFixed(2)}</strong>`;
            container.appendChild(samuelEl);

            const otherPeople = Object.keys(breakdown).filter(p => p !== 'Samuel');
            if (otherPeople.length > 0) {
                const titleEl = document.createElement('h3');
                titleEl.className = 'other-payments-title';
                titleEl.innerText = 'Otros Pagos';
                container.appendChild(titleEl);

                const othersContainer = document.createElement('div');
                othersContainer.className = 'other-payments';
                otherPeople.forEach(person => {
                    const personEl = document.createElement('p');
                    personEl.innerHTML = `${person}: <strong>$${breakdown[person].toFixed(2)}</strong>`;
                    othersContainer.appendChild(personEl);
                });
                container.appendChild(othersContainer);
            }
        }

        // --- NAVIGATION & DISPLAY ---
        function updateMonthDisplay() {
            const header = document.getElementById('history-month-year');
            header.innerText = displayedDate.toLocaleString('es-MX', { month: 'long', year: 'numeric' });
        }
        function showPreviousMonth() {
            displayedDate.setMonth(displayedDate.getMonth() - 1);
            renderAll();
        }
        function showNextMonth() {
            displayedDate.setMonth(displayedDate.getMonth() + 1);
            renderAll();
        }

        // --- CORE LOGIC & EVENT HANDLERS ---
        function addCard() {
            const newCard = {
                id: Date.now(),
                name: 'Nueva Tarjeta',
                limit: 5000,
                cutDay: 1,
                payDay: 20,
                color: `#${Math.floor(Math.random()*16777215).toString(16).padStart(6, '0')}`
            };
            cards.push(newCard);
            saveData();
            renderAll();
        }

        function updateCardDetail(cardId, key, value) {
            const card = cards.find(c => c.id === cardId);
            if (card) {
                if(key === 'limit' || key === 'cutDay' || key === 'payDay') {
                    const numValue = parseInt(value.replace(/[^0-9]/g, ''), 10);
                    card[key] = isNaN(numValue) ? card[key] : numValue;
                } else {
                    card[key] = value;
                }
                saveData();
                renderAll();
            }
        }
        
        function deleteCard(cardId) {
            if (confirm('¿Estás seguro? Se eliminará la tarjeta y todos sus gastos asociados.')) {
                cards = cards.filter(c => c.id !== cardId);
                expenses = expenses.filter(e => e.cardId !== cardId);
                saveData();
                renderAll();
            }
        }

        function deleteExpense(expenseId) {
            if (confirm('¿Estás seguro de que quieres eliminar este gasto?')) {
                expenses = expenses.filter(exp => exp.id !== expenseId);
                saveData();
                renderAll();
            }
        }

        function addPerson() {
            const nameInput = document.getElementById('new-person-name');
            const name = nameInput.value.trim();
            if (name && !people.includes(name)) {
                people.push(name);
                nameInput.value = '';
                saveData();
                renderPeople();
            }
        }

        function populateRegistrationMonthSelect(selectElId, selectedDate = new Date()) {
            const select = document.getElementById(selectElId);
            select.innerHTML = '';
            const now = new Date();
            for (let i = -6; i <= 12; i++) {
                const date = new Date(now.getFullYear(), now.getMonth() + i, 1);
                const month = date.getMonth();
                const year = date.getFullYear();
                const option = document.createElement('option');
                option.value = `${month}-${year}`;
                option.innerText = date.toLocaleString('es-MX', { month: 'long', year: 'numeric' });
                if (date.getMonth() === selectedDate.getMonth() && date.getFullYear() === selectedDate.getFullYear()) {
                    option.selected = true;
                }
                select.appendChild(option);
            }
        }

        function openExpenseForm() {
            if (cards.length === 0) {
                alert("Primero debes agregar una tarjeta de crédito.");
                return;
            }
            document.getElementById('modal-title').innerText = 'Nuevo Gasto';
            document.getElementById('modal-submit-button').innerText = 'Registrar Gasto';
            document.getElementById('editing-expense-id').value = '';
            document.getElementById('expense-description').value = '';
            document.getElementById('expense-amount').value = '';
            document.getElementById('payment-type').value = 'single';
            populateRegistrationMonthSelect('expense-date', new Date());
            toggleDeferredOptions();
            document.getElementById('expense-form-overlay').classList.add('active');
        }

        function editExpense(expenseId) {
            const expense = expenses.find(exp => exp.id === expenseId);
            if (!expense) return;

            document.getElementById('modal-title').innerText = 'Editar Gasto';
            document.getElementById('modal-submit-button').innerText = 'Guardar Cambios';
            document.getElementById('editing-expense-id').value = expense.id;
            document.getElementById('expense-description').value = expense.description;
            document.getElementById('expense-amount').value = expense.amount;
            document.getElementById('expense-card').value = expense.cardId;
            document.getElementById('expense-person').value = expense.person;
            document.getElementById('payment-type').value = expense.type;
            populateRegistrationMonthSelect('expense-date', new Date(expense.date));
            
            toggleDeferredOptions();
            if (expense.type === 'deferred') {
                document.getElementById('total-installments').value = expense.totalInstallments;
                document.getElementById('current-installment').value = expense.currentInstallment;
            }

            document.getElementById('expense-form-overlay').classList.add('active');
        }

        function closeExpenseForm() {
            document.getElementById('expense-form-overlay').classList.remove('active');
        }

        document.getElementById('expense-form-overlay').addEventListener('click', (event) => {
            if (event.target.id === 'expense-form-overlay') {
                closeExpenseForm();
            }
        });
        
        function updateCardOptionsInForm() {
            const select = document.getElementById('expense-card');
            select.innerHTML = cards.map(c => `<option value="${c.id}">${c.name}</option>`).join('');
        }

        function toggleDeferredOptions() {
            const type = document.getElementById('payment-type').value;
            const deferredOptions = document.getElementById('deferred-options');
            const amountLabel = document.getElementById('amount-label');
            if (type === 'deferred') {
                deferredOptions.style.display = 'block';
                amountLabel.innerText = 'Monto Mensual';
            } else {
                deferredOptions.style.display = 'none';
                amountLabel.innerText = 'Monto Total';
            }
        }

        function processExpense() {
            const editingId = parseInt(document.getElementById('editing-expense-id').value);
            const description = document.getElementById('expense-description').value;
            const amount = parseFloat(document.getElementById('expense-amount').value);
            
            if (!description || isNaN(amount) || amount <= 0) {
                alert("Por favor, completa la descripción y un monto válido.");
                return;
            }
            
            const [month, year] = document.getElementById('expense-date').value.split('-').map(Number);
            const registrationDate = new Date(year, month, 15);

            const expenseData = {
                description,
                amount,
                cardId: parseInt(document.getElementById('expense-card').value),
                person: document.getElementById('expense-person').value,
                type: document.getElementById('payment-type').value,
                date: registrationDate.toISOString(),
                paid: false // Always reset to unpaid on edit/add
            };

            if (expenseData.type === 'deferred') {
                expenseData.totalInstallments = parseInt(document.getElementById('total-installments').value);
                expenseData.currentInstallment = parseInt(document.getElementById('current-installment').value);
                if (expenseData.currentInstallment > expenseData.totalInstallments) {
                    alert("El mes actual no puede ser mayor al total de meses.");
                    return;
                }
            }

            if (editingId) {
                const index = expenses.findIndex(exp => exp.id === editingId);
                if (index > -1) {
                    expenses[index] = { ...expenses[index], ...expenseData };
                }
            } else {
                expenseData.id = Date.now();
                expenses.push(expenseData);
            }
            
            saveData();
            renderAll();
            closeExpenseForm();
        }

        function togglePaymentStatus(expenseId) {
            const expense = expenses.find(exp => exp.id === expenseId);
            if (expense) {
                expense.paid = !expense.paid;
                saveData();
                renderAll();
            }
        }

        // --- CALCULATION FUNCTIONS (REVISED & CORRECTED) ---
        function getDueExpensesForDate(referenceDate, onlyUnpaid = false) {
            let dueExpenses = [];

            expenses.forEach(expense => {
                let isDue = false;

                if (expense.type === 'single') {
                    const expenseDate = new Date(expense.date);
                    if (expenseDate.getMonth() === referenceDate.getMonth() && expenseDate.getFullYear() === referenceDate.getFullYear()) {
                        isDue = true;
                    }
                } else if (expense.type === 'deferred') {
                    const registrationDate = new Date(expense.date);
                    const firstInstallmentDate = new Date(registrationDate.getFullYear(), registrationDate.getMonth() - (expense.currentInstallment - 1), 1);
                    const monthsPassed = (referenceDate.getFullYear() - firstInstallmentDate.getFullYear()) * 12 + (referenceDate.getMonth() - firstInstallmentDate.getMonth());
                    const installmentNumberForRefDate = monthsPassed + 1;

                    if (installmentNumberForRefDate > 0 && installmentNumberForRefDate <= expense.totalInstallments) {
                        isDue = true;
                    }
                }

                if (isDue) {
                    dueExpenses.push(expense);
                }
            });

            if (onlyUnpaid) {
                return dueExpenses.filter(exp => !exp.paid);
            }
            return dueExpenses;
        }

        function getPaymentBreakdownForDate(referenceDate, onlyUnpaid = false) {
            const breakdown = {};
            const dueExpenses = getDueExpensesForDate(referenceDate, onlyUnpaid);
            
            dueExpenses.forEach(expense => {
                if (!breakdown[expense.person]) {
                    breakdown[expense.person] = 0;
                }
                breakdown[expense.person] += expense.amount;
            });
            return breakdown;
        }

        function calculateTotalDueForCard(cardId, referenceDate) {
            const dueExpenses = getDueExpensesForDate(referenceDate, true); // Only unpaid
            return dueExpenses
                .filter(expense => expense.cardId === cardId)
                .reduce((total, expense) => total + expense.amount, 0);
        }

        function calculateTotalDebt(cardId) {
            let totalDebt = 0;
            expenses.forEach(expense => {
                if (expense.cardId !== cardId) return;

                if (expense.type === 'single' && !expense.paid) {
                    totalDebt += expense.amount;
                } else if (expense.type === 'deferred') {
                    const registrationDate = new Date(expense.date);
                    const firstInstallmentDate = new Date(registrationDate.getFullYear(), registrationDate.getMonth() - (expense.currentInstallment - 1), 1);
                    const now = new Date();
                    
                    if (now >= firstInstallmentDate) {
                        const monthsPassed = (now.getFullYear() - firstInstallmentDate.getFullYear()) * 12 + (now.getMonth() - firstInstallmentDate.getMonth());
                        const currentInstallmentNumber = monthsPassed + 1;

                        if (currentInstallmentNumber > 0 && currentInstallmentNumber <= expense.totalInstallments) {
                            const remainingInstallments = expense.totalInstallments - currentInstallmentNumber + 1;
                            totalDebt += expense.amount * remainingInstallments;
                        }
                    }
                }
            });
            return totalDebt;
        }

        // --- PROJECTION FUNCTIONS ---
        function renderNextMonthProjection() {
            const now = displayedDate;
            const nextMonthDate = new Date(now.getFullYear(), now.getMonth() + 1, 1);
            const nextMonth = nextMonthDate.getMonth();
            const nextYear = nextMonthDate.getFullYear();

            const breakdown = calculateFutureProjectionByPerson(nextMonth, nextYear);
            const container = document.getElementById('projection-result');
            container.innerHTML = '';

            const nextMonthName = nextMonthDate.toLocaleString('es-MX', { month: 'long' });
            const titleEl = document.createElement('h2');
            titleEl.innerHTML = `Proyección para <strong>${nextMonthName}</strong>`;
            container.appendChild(titleEl);

            const total = Object.values(breakdown).reduce((sum, val) => sum + val, 0);
            const totalEl = document.createElement('p');
            totalEl.className = 'payment-breakdown-total';
            totalEl.innerHTML = `Total: <strong>$${total.toFixed(2)}</strong>`;
            container.appendChild(totalEl);
            
            const samuelTotal = breakdown['Samuel'] || 0;
            const samuelEl = document.createElement('p');
            samuelEl.className = 'payment-breakdown-samuel';
            samuelEl.innerHTML = `Samuel: <strong>$${samuelTotal.toFixed(2)}</strong>`;
            container.appendChild(samuelEl);

            const otherPeople = Object.keys(breakdown).filter(p => p !== 'Samuel');
            if (otherPeople.length > 0) {
                const othersTitleEl = document.createElement('h3');
                othersTitleEl.className = 'other-payments-title';
                othersTitleEl.innerText = 'Otros Pagos Proyectados';
                container.appendChild(othersTitleEl);

                const othersContainer = document.createElement('div');
                othersContainer.className = 'other-payments';
                otherPeople.forEach(person => {
                    const personEl = document.createElement('p');
                    personEl.innerHTML = `${person}: <strong>$${breakdown[person].toFixed(2)}</strong>`;
                    othersContainer.appendChild(personEl);
                });
                container.appendChild(othersContainer);
            }
        }

        function calculateFutureProjectionByPerson(targetMonth, targetYear) {
            const breakdown = {};
            const targetDate = new Date(targetYear, targetMonth, 1);

            expenses.forEach(exp => {
                if (exp.type !== 'deferred') return;

                const registrationDate = new Date(exp.date);
                const firstInstallmentDate = new Date(registrationDate.getFullYear(), registrationDate.getMonth() - (exp.currentInstallment - 1), 1);

                if (targetDate < firstInstallmentDate) return;

                const monthsPassed = (targetDate.getFullYear() - firstInstallmentDate.getFullYear()) * 12 + (targetDate.getMonth() - firstInstallmentDate.getMonth());
                const installmentNumberInFuture = monthsPassed + 1;

                if (installmentNumberInFuture > 0 && installmentNumberInFuture <= exp.totalInstallments) {
                    if (!breakdown[exp.person]) breakdown[exp.person] = 0;
                    breakdown[exp.person] += exp.amount;
                }
            });
            return breakdown;
        }
        
        function getProjectedDeferredExpensesForDate(targetDate) {
            const projectedExpenses = [];
            
            expenses.forEach(exp => {
                if (exp.type !== 'deferred') return;
                
                const registrationDate = new Date(exp.date);
                const firstInstallmentDate = new Date(registrationDate.getFullYear(), registrationDate.getMonth() - (exp.currentInstallment - 1), 1);
                if (targetDate < firstInstallmentDate) return;

                const monthsPassed = (targetDate.getFullYear() - firstInstallmentDate.getFullYear()) * 12 + (targetDate.getMonth() - firstInstallmentDate.getMonth());
                const installmentNumberInFuture = monthsPassed + 1;

                if (installmentNumberInFuture > 0 && installmentNumberInFuture <= exp.totalInstallments) {
                    projectedExpenses.push({
                        ...exp,
                        isProjection: true,
                        currentInstallment: installmentNumberInFuture,
                    });
                }
            });
            return projectedExpenses;
        }

        // --- EXPORT FUNCTIONS ---
        function exportToCSV() {
            let csvContent = "data:text/csv;charset=utf-8,";
            csvContent += "Mes de Registro,Descripcion,Monto,Persona,Tarjeta,Tipo de Pago,Mes Actual,Total Meses,Pagado\r\n";
            expenses.forEach(exp => {
                const card = cards.find(c => c.id === exp.cardId);
                const monthYear = new Date(exp.date).toLocaleString('es-MX', { month: 'long', year: 'numeric' });
                const row = [
                    `"${monthYear}"`,
                    `"${exp.description.replace(/"/g, '""')}"`,
                    exp.amount,
                    exp.person,
                    card ? `"${card.name}"` : "N/A",
                    exp.type,
                    exp.currentInstallment || 'N/A',
                    exp.totalInstallments || 'N/A',
                    exp.paid ? 'Si' : 'No'
                ].join(",");
                csvContent += row + "\r\n";
            });

            const encodedUri = encodeURI(csvContent);
            const link = document.createElement("a");
            link.setAttribute("href", encodedUri);
            link.setAttribute("download", "reporte_financiero.csv");
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        }

        function exportToText() {
            let textContent = "Reporte Financiero\n====================\n\n";
            const expensesByMonth = {};
            expenses.forEach(exp => {
                const monthYear = new Date(exp.date).toLocaleString('es-MX', { month: 'long', year: 'numeric' });
                if (!expensesByMonth[monthYear]) expensesByMonth[monthYear] = [];
                expensesByMonth[monthYear].push(exp);
            });

            const sortedMonths = Object.keys(expensesByMonth).sort((a, b) => new Date(`1 ${b.replace(' de ', ' ')}`) - new Date(`1 ${a.replace(' de ', ' ')}`));

            sortedMonths.forEach(month => {
                textContent += `\n--- ${month.charAt(0).toUpperCase() + month.slice(1)} ---\n`;
                expensesByMonth[month].forEach(exp => {
                    const card = cards.find(c => c.id === exp.cardId);
                    textContent += ` - ${exp.description}: $${exp.amount.toFixed(2)}`;
                    if (exp.type === 'deferred') {
                        textContent += ` (Mensualidad ${exp.currentInstallment} de ${exp.totalInstallments}) en [${card ? card.name : 'N/A'}] por ${exp.person}\n`;
                    } else {
                        textContent += ` (Pago Único) en [${card ? card.name : 'N/A'}] por ${exp.person}\n`;
                    }
                });
            });

            const blob = new Blob([textContent], { type: 'text/plain;charset=utf-8' });
            const link = document.createElement("a");
            link.href = URL.createObjectURL(blob);
            link.download = "reporte_financiero.txt";
            link.click();
            URL.revokeObjectURL(link.href);
        }

        // --- INITIAL LOAD ---
        document.addEventListener('DOMContentLoaded', () => {
            if (cards.length === 0) {
                 cards.push({ id: 1, name: 'Mi Tarjeta Azul', limit: 10000, cutDay: 15, payDay: 5, color: '#007bff' });
            }
            displayCurrentDate();
            renderAll();
        });
    </script>
</body>
</html>
