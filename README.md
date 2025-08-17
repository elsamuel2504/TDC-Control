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
            font-size: 1.8em;
            font-weight: 300;
        }

        .main-summary-section {
            text-align: center;
            background-color: var(--secondary-color);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 40px;
        }
        .main-summary-section h2 {
            margin-top: 0;
            font-size: 1.2em;
            font-weight: 300;
            color: #b0b0b0;
        }
        .main-summary-section p {
            font-size: 2.5em;
            font-weight: bold;
            color: var(--accent-color);
            margin: 0;
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
        
        .tabs {
            display: flex;
            border-bottom: 1px solid #444;
            margin-bottom: 20px;
        }

        .tab-button {
            padding: 10px 20px;
            cursor: pointer;
            background: none;
            border: none;
            color: #b0b0b0;
            border-bottom: 3px solid transparent;
            transition: color 0.2s, border-color 0.2s;
        }

        .tab-button.active {
            color: var(--accent-color);
            border-bottom-color: var(--accent-color);
        }
        
        .month-content { display: none; }
        .month-content.active { display: block; }

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

    </style>
</head>
<body>

    <div class="container">
        <div class="welcome-header">
            <h1>Bienvenido, Samuel</h1>
        </div>

        <div class="main-summary-section">
            <h2>Total a Pagar este Mes</h2>
            <p id="total-monthly-payment">$0.00</p>
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
            <h2>Historial de Gastos</h2>
            <div class="tabs" id="month-tabs">
                <!-- Las pestañas de los meses se generarán aquí -->
            </div>
            <div id="expenses-by-month">
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
            <h2 style="margin-top:0;">Nuevo Gasto</h2>
            <div class="form-group">
                <label for="expense-description">Descripción</label>
                <input type="text" id="expense-description" required>
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
            <button class="btn btn-primary" onclick="addExpense()">Registrar Gasto</button>
        </div>
    </div>
    
    <script>
        // --- DATA MODEL & PERSISTENCE ---
        let cards = JSON.parse(localStorage.getItem('cards')) || [
            { id: 1, name: 'Mi Tarjeta Azul', limit: 10000, cutDay: 15, payDay: 5, color: '#007bff' },
            { id: 2, name: 'Tarjeta Verde', limit: 15000, cutDay: 20, payDay: 10, color: '#28a745' },
            { id: 3, name: 'La Dorada', limit: 20000, cutDay: 1, payDay: 21, color: '#ffc107' }
        ];
        let expenses = JSON.parse(localStorage.getItem('expenses')) || [];
        let people = JSON.parse(localStorage.getItem('people')) || ['Samuel'];

        function saveData() {
            localStorage.setItem('cards', JSON.stringify(cards));
            localStorage.setItem('expenses', JSON.stringify(expenses));
            localStorage.setItem('people', JSON.stringify(people));
        }

        // --- RENDER FUNCTIONS ---
        function renderAll() {
            renderCards();
            renderPeople();
            renderExpensesByMonth();
            renderTotalMonthlyPayment();
        }

        function renderCards() {
            const container = document.getElementById('cards-container');
            container.innerHTML = '';
            cards.forEach(card => {
                const totalDebt = calculateTotalDebt(card.id);
                const remainingBalance = card.limit - totalDebt;
                const paymentDue = calculateTotalDueForCard(card.id);
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

        function renderExpensesByMonth() {
            const tabsContainer = document.getElementById('month-tabs');
            const contentContainer = document.getElementById('expenses-by-month');
            tabsContainer.innerHTML = '';
            contentContainer.innerHTML = '';

            const expensesByMonth = {};
            expenses.forEach(exp => {
                const monthYear = new Date(exp.date).toLocaleString('es-MX', { month: 'long', year: 'numeric' });
                if (!expensesByMonth[monthYear]) {
                    expensesByMonth[monthYear] = [];
                }
                expensesByMonth[monthYear].push(exp);
            });

            const sortedMonths = Object.keys(expensesByMonth).sort((a, b) => {
                const dateA = new Date(`1 ${a.replace(' de ', ' ')}`);
                const dateB = new Date(`1 ${b.replace(' de ', ' ')}`);
                return dateB - dateA;
            });

            sortedMonths.forEach((month, index) => {
                const tabId = month.replace(/[^a-zA-Z0-9]/g, '');
                const tab = document.createElement('button');
                tab.className = 'tab-button';
                tab.innerText = month.charAt(0).toUpperCase() + month.slice(1);
                tab.onclick = () => switchTab(tabId);
                
                const content = document.createElement('div');
                content.id = tabId;
                content.className = 'month-content';
                
                let tableHTML = '<table><thead><tr><th>Descripción</th><th>Monto</th><th>Persona</th><th>Tarjeta</th><th>Tipo</th><th>Acciones</th></tr></thead><tbody>';
                expensesByMonth[month].forEach(exp => {
                    const card = cards.find(c => c.id === exp.cardId);
                    let paymentInfo = exp.type === 'single' ? 'Único' : `Diferido (${exp.currentInstallment}/${exp.totalInstallments})`;
                    let amountDisplay = exp.type === 'single' ? exp.amount : exp.amount; // Amount is monthly for deferred
                    tableHTML += `<tr>
                        <td>${exp.description}</td>
                        <td>$${amountDisplay.toFixed(2)}</td>
                        <td>${exp.person}</td>
                        <td>${card ? card.name : 'N/A'}</td>
                        <td>${paymentInfo}</td>
                        <td><button class="btn-delete-expense" onclick="deleteExpense(${exp.id})">Eliminar</button></td>
                    </tr>`;
                });
                tableHTML += '</tbody></table>';
                content.innerHTML = tableHTML;
                
                tabsContainer.appendChild(tab);
                contentContainer.appendChild(content);

                if (index === 0) {
                    tab.classList.add('active');
                    content.classList.add('active');
                }
            });
        }
        
        function renderTotalMonthlyPayment() {
            const totalPayment = cards.reduce((total, card) => {
                return total + calculateTotalDueForCard(card.id);
            }, 0);
            document.getElementById('total-monthly-payment').innerText = `$${totalPayment.toFixed(2)}`;
        }

        function switchTab(tabId) {
            document.querySelectorAll('.tab-button').forEach(b => b.classList.remove('active'));
            document.querySelectorAll('.month-content').forEach(c => c.classList.remove('active'));
            
            const activeTab = Array.from(document.querySelectorAll('.tab-button')).find(b => b.innerText.replace(/[^a-zA-Z0-9]/g, '') === tabId);
            if(activeTab) activeTab.classList.add('active');
            
            const activeContent = document.getElementById(tabId);
            if(activeContent) activeContent.classList.add('active');
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

        function openExpenseForm() {
            if (cards.length === 0) {
                alert("Primero debes agregar una tarjeta de crédito.");
                return;
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

        function addExpense() {
            const description = document.getElementById('expense-description').value;
            const amount = parseFloat(document.getElementById('expense-amount').value);
            if (!description || isNaN(amount) || amount <= 0) {
                alert("Por favor, completa la descripción y un monto válido.");
                return;
            }

            const newExpense = {
                id: Date.now(),
                description,
                amount,
                cardId: parseInt(document.getElementById('expense-card').value),
                person: document.getElementById('expense-person').value,
                type: document.getElementById('payment-type').value,
                date: new Date().toISOString()
            };

            if (newExpense.type === 'deferred') {
                newExpense.totalInstallments = parseInt(document.getElementById('total-installments').value);
                newExpense.currentInstallment = parseInt(document.getElementById('current-installment').value);
                if (newExpense.currentInstallment > newExpense.totalInstallments) {
                    alert("El mes actual no puede ser mayor al total de meses.");
                    return;
                }
            }
            
            expenses.push(newExpense);
            saveData();
            renderAll();
            closeExpenseForm();
            // Reset form fields
            document.getElementById('expense-description').value = '';
            document.getElementById('expense-amount').value = '';
            document.getElementById('payment-type').value = 'single';
            toggleDeferredOptions();
        }

        // --- CALCULATION FUNCTIONS (CORRECTED LOGIC) ---
        function calculateTotalDebt(cardId) {
            return expenses.reduce((total, expense) => {
                if (expense.cardId !== cardId) {
                    return total;
                }
                if (expense.type === 'single') {
                    return total + expense.amount;
                }
                if (expense.type === 'deferred') {
                    const remainingInstallments = (expense.totalInstallments - expense.currentInstallment) + 1;
                    return total + (expense.amount * remainingInstallments);
                }
                return total;
            }, 0);
        }

        function calculateTotalDueForCard(cardId) {
            const card = cards.find(c => c.id === cardId);
            if (!card) return 0;

            const today = new Date();
            const currentYear = today.getFullYear();
            const currentMonth = today.getMonth(); // 0-11

            let cutOffDate;
            if (today.getDate() > card.cutDay) {
                cutOffDate = new Date(currentYear, currentMonth, card.cutDay, 23, 59, 59);
            } else {
                cutOffDate = new Date(currentYear, currentMonth - 1, card.cutDay, 23, 59, 59);
            }

            let lastCutOffDate = new Date(cutOffDate);
            lastCutOffDate.setMonth(lastCutOffDate.getMonth() - 1);

            let totalDue = 0;
            expenses.forEach(expense => {
                if (expense.cardId !== cardId) return;

                const expenseDate = new Date(expense.date);

                if (expense.type === 'single') {
                    if (expenseDate > lastCutOffDate && expenseDate <= cutOffDate) {
                        totalDue += expense.amount;
                    }
                } else if (expense.type === 'deferred') {
                    // Check if any installment of this deferred payment falls into the current billing cycle
                    for (let i = 0; i < expense.totalInstallments; i++) {
                        const installmentDate = new Date(expense.date);
                        installmentDate.setMonth(installmentDate.getMonth() + i - (expense.currentInstallment - 1));
                        
                        if (installmentDate > lastCutOffDate && installmentDate <= cutOffDate) {
                            totalDue += expense.amount; // Add the fixed monthly amount
                            break; // Count only one installment per cycle
                        }
                    }
                }
            });
            return totalDue;
        }

        // --- EXPORT FUNCTIONS ---
        function exportToCSV() {
            let csvContent = "data:text/csv;charset=utf-8,";
            csvContent += "Mes,Descripcion,Monto,Persona,Tarjeta,Tipo de Pago,Mes Actual,Total Meses\r\n";
            expenses.forEach(exp => {
                const card = cards.find(c => c.id === exp.cardId);
                const monthYear = new Date(exp.date).toLocaleString('es-MX', { month: 'long', year: 'numeric' });
                const row = [
                    `"${monthYear}"`,
                    `"${exp.description.replace(/"/g, '""')}"`,
                    exp.amount, // This is the monthly amount for deferred
                    exp.person,
                    card ? `"${card.name}"` : "N/A",
                    exp.type,
                    exp.currentInstallment || 'N/A',
                    exp.totalInstallments || 'N/A'
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
        document.addEventListener('DOMContentLoaded', renderAll);
    </script>
</body>
</html>
