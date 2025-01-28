<script setup>

import axios from 'axios';
document.addEventListener('DOMContentLoaded', () => {
    const chatBotIcon = document.getElementById('chatBotIcon');
    const chatModal = document.getElementById('chatModal');
    const closeModal = document.getElementById('closeModal');
    const userInput = document.getElementById('userInput');
    const sendMessage = document.getElementById('sendMessage');
    const chatContent = document.getElementById('chatContent');
    const importButton = document.getElementById('importButton');
    const exportButton = document.getElementById('exportButton');
    // const clear = document.getElementById('clear');
    chatBotIcon.addEventListener('click', () => {
        chatModal.classList.toggle('hidden');
    });
    closeModal.addEventListener('click', () => {
        chatModal.classList.add('hidden');
    });
    // clear.addEventListener('click', () => {
    //     localStorage.clear();
    //     const chatContent = document.getElementById('chatContent');
    //     chatContent.innerHTML = '';
    // });
    sendMessage.addEventListener('click', async () => {
        const message = userInput.value.trim();
        const messageDiv = document.createElement('div');
        const div1 = document.createElement('div');
        messageDiv.className = 'mt-12';
        messageDiv.id = 'message'
        div1.classList.add('text-right', 'float-right', 'p-2', 'text-wrap', 'overflow-wrap', 'max-w-screen-sm');
        div1.style.fontFamily = 'Roboto Slab'
        div1.style.background = '#EFF2FF'
        div1.style.color = '#2B48B0'
        div1.style.borderRadius = '10px'
        div1.style.borderTopRightRadius = '0px'
        div1.style.fontSize = '14px'
        div1.textContent = message;  // Ответ от чат-бота
        messageDiv.appendChild(div1)
        chatContent.appendChild(messageDiv);
        if (message) {
            try {
                const response = await axios.post('http://127.0.0.1:5000/chat', {
                    message: message
                }, {
                    headers: {
                        'Content-Type': 'application/json'
                    }
                });
                // Получаем ответ от сервера и выводим его
                const responseMessage = document.createElement('div');
                const div1 = document.createElement('div');
                responseMessage.id = 'message'
                div1.classList.add('text-left', 'rounded-lg', 'float-left', 'p-2', 'text-wrap', 'overflow-wrap', 'max-w-screen-sm');
                div1.style.fontFamily = 'Roboto Slab'
                div1.style.fontSize = '14px'
                div1.style.backgroundColor = '#CFDFFF'
                div1.style.color = '#2B48B0'
                div1.style.borderRadius = '10px'
                div1.style.borderTopLeftRadius = '0px'
                div1.textContent = response.data.response;  // Ответ от чат-бота
                // Сохраняем в localStorage
                const responseMessageKey = 'responseMessage_' + new Date().getTime();
                localStorage.setItem(responseMessageKey, responseMessage.outerHTML);
                // Добавляем сообщение на страницу
                responseMessage.appendChild(div1)
                chatContent.appendChild(responseMessage);
            } catch (error) {
                console.error('Error sending message:', error);
            }
        }
    });
    // Загрузка файла
    importButton.addEventListener('click', async () => {
        const messages = document.querySelectorAll('#message');
        const chatHistory = [];
        messages.forEach(message => {
            chatHistory.push({ textContent: message.textContent});
        });
        try {
            const response = await axios.post('http://127.0.0.1:5000/import', {
                message: chatHistory
            }, {
                headers: {
                    'Content-Type': 'application/json'
                }
            });
            console.log(response.data);
            const result = await response.data;
            console.log(result);
            const jsonContent = JSON.stringify(chatHistory, null, 2);
            const blob = new Blob([jsonContent], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'chatHistory.json';
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            alert(result.message || result.error);
        } catch (error) {
            console.error('Error sending message:', error);
        }
    });
    // Выгрузка файла
    exportButton.addEventListener('change', () => {
        const fileInput = document.getElementById('exportButton');
        const file = fileInput.files[0];
        if (file) {
            const reader = new FileReader();
            reader.onload = function(event) {
                const jsonContent = event.target.result;
                const chatHistory = JSON.parse(jsonContent);
                const chatContainer = document.getElementById('chatContent');
                chatContainer.innerHTML = ''; // Очистить контейнер перед добавлением новых элементов
                chatHistory.forEach((message, index) => {
                    const messageDiv = document.createElement('div');
                    const div1 = document.createElement('div');
                    const div2 = document.createElement('div');
                    messageDiv.className = 'mt-12';
                    messageDiv.id = 'message'
                    if (index % 2 == 0) {
                        div2.classList.add('text-right', 'bg-blue-300', 'rounded-lg', 'float-right', 'p-2', 'rounded-br-none', 'text-wrap', 'overflow-wrap', 'max-w-screen-sm');
                        div2.textContent = message.textContent;
                        messageDiv.appendChild(div2)
                    } else {
                        div1.classList.add('text-left', 'bg-blue-400', 'rounded-lg', 'float-left', 'p-2', 'rounded-bl-none', 'text-wrap', 'overflow-wrap', 'max-w-screen-sm');
                        div1.textContent = message.textContent;
                        messageDiv.appendChild(div1)
                    }
                    chatContainer.appendChild(messageDiv);
                });
            };
            reader.readAsText(file);
        }
    });
    // Драггинг
    // const draggable = document.getElementById('chatModalBg');
    // draggable.addEventListener('mousedown', function(e) {
    //     let shiftX = e.clientX - draggable.getBoundingClientRect().left;
    //     let shiftY = e.clientY - draggable.getBoundingClientRect().top;
    //     function moveAt(pageX, pageY) {
    //         draggable.style.left = pageX - shiftX + 'px';
    //         draggable.style.top = pageY - shiftY + 'px';
    //     }
    //     function onMouseMove(event) {
    //         moveAt(event.pageX, event.pageY);
    //     }
    //     document.addEventListener('mousemove', onMouseMove);
    //     draggable.onmouseup = function() {
    //         document.removeEventListener('mousemove', onMouseMove);
    //         draggable.onmouseup = null;
    //     };
    // });
    // draggable.ondragstart = function() {
    //     return false;
    // };
});
</script>
<template>
 <div class="fixed" style="right: 5%; bottom: 5%; width: 10%;">    <!-- chat Bot button -->
        <button id="chatBotIcon"> <img src="../assets/images/Filicia_suite_a.gif"></button>
    </div>

    <div id="chatModal" class="fixed inset-0 bg-opacity-75 flex items-center justify-centertop-1/4" style="left: 67%; height: 80%; width: 32%; top: 19%; transform-origin: bottom right; background-color:#1C356E; border-radius: 10px;">
        <h2 style="font-family: Roboto Slab; padding-left: 5.2%; font-size: 100%; position: absolute; top: 1.6%; color: gainsboro; user-select: none;">Фeлиция 0.1</h2>  <!-- logo chat bot-->
        <div style="width: 26.1%; position: absolute; top: 6%; left: 5%;  user-select: none;"><img src="../assets/images/line_police.svg"></div>
        <img src="../assets/images/logo_gerb_a.png" style="position: absolute; top: 0%; height: 10%; z-index: -1; left: 27%;  user-select: none;">
        <button id="closeModal"><img src="../assets/images/close_gpt_chat.png" style="position: absolute; width: 2.6%; left: 93.5%; top: 3%;  user-select: none;"></button>
        <div id="chatModalBg" style="background-color: #E7EAF2; position: absolute;left: 1.4% ;width: 97%; height: 60%; border-radius: 9px; top: 8.5%; border-bottom-right-radius: 0px; border-bottom-left-radius: 0px;"> 
                
            <div id="chatContent" class="overflow-y-auto flex-grow space-y-4 flex flex-col" style="padding-left: 15px; padding-right: 25px; max-height: 100%;">     
                <div id="message" class="mt-5" style=" max-width: 80%;">  <!--- Указать максимальную ширину для всех сообщений 80%;--->
                    <div class="text-left rounded-lg float-left p-2 text-wrap overflow-wrap max-w-screen-sm"
                    style="font-family: Roboto Slab; font-size: 14px; background-color: #CFDFFF; color: #2B48B0;  border-radius: 10px; border-top-left-radius: 0px;">
                        Робот Фелиция поможет в решении ваших вопросов. Я во внимании!
                    </div>
                </div>
<!-- Dlya Romi $$$$$$$$$$$$$$$$$-->   <!--- Плюс не юзай break-all так как сообщения переносятся по буквам, а не по словам --->
                <div class="mt-12" id="message" style="font-family: Roboto Slab; font-size: 15px;">
                    <div class="text-left float-right p-2 text-wrap overflow-wrap max-w-screen-sm" style="background: #EFF2FF; color: #2B48B0; border-radius: 10px; border-top-right-radius: 0px; font-size: 14px;  max-width: 80%;">Как восстановить пароль к учетным записям ИСОД МВД России ОПБ Катаева?</div>
                </div>
<!-- Dlya Romi $$$$$$$$$$$$$$$$$$$-->        
<div id="message" class="mt-5" style=" max-width: 80%;">  <!--- Указать максимальную ширину для всех сообщений 80%;--->
                    <div class="text-left rounded-lg float-left p-2 text-wrap overflow-wrap max-w-screen-sm"
                    style="font-family: Roboto Slab; font-size: 14px; background-color: #CFDFFF; color: #2B48B0;  border-radius: 10px; border-top-left-radius: 0px;">
                    Нужно отправить заявку на восстановление пароля. Желаете оставить заявку?
                    </div>
                </div>
<!-- Dlya Romi $$$$$$$$$$$$$$$$$-->   <!--- Плюс не юзай break-all так как сообщения переносятся по буквам, а не по словам --->
                <div class="mt-12" id="message" style="font-family: Roboto Slab; font-size: 15px;">
                    <div class="text-right float-right p-2  text-wrap overflow-wrap max-w-screen-sm" style="background: #EFF2FF; color: #2B48B0; border-radius: 10px; border-top-right-radius: 0px; font-size: 14px;">Да</div>
                </div>
                <div id="message" class="mt-5" style=" max-width: 80%;">  <!--- Указать максимальную ширину для всех сообщений 80%;--->
                    <div class="text-left rounded-lg float-left p-2 text-wrap overflow-wrap max-w-screen-sm"
                    style="font-family: Roboto Slab; font-size: 14px; background-color: #CFDFFF; color: #2B48B0;  border-radius: 10px; border-top-left-radius: 0px;">
                    Заявка №11247 принята и находится в обработке Единым центром эксплуатации (ЕЦЭ).
                    </div>
                </div>
<!-- Dlya Romi $$$$$$$$$$$$$$$$$-->   <!--- Плюс не юзай break-all так как сообщения переносятся по буквам, а не по словам --->
             </div>
        </div>
        <div class="bottom_chat" style="width: 97%; position: absolute; left: 1.4%; background: #E7EAF2; height: 50%; bottom: 1.5%; border-radius: 9px; z-index: -1; "> 
         
            <div class="p-2 flex-shrink-0" style="background-color: white; height: 50%; width: 70%; border-radius: 15px; position: absolute; right:2%; bottom: 2%;">
                <textarea id="userInput" style=" width: 100%;  height: 70%; resize: none; padding-top: 7px; padding-left: 10px; outline: none; font-family: Roboto Slab; color: #4D4F5B;" placeholder="Задайте ваш вопрос..."> </textarea> 
                <button id="sendMessage" class=" text-white p-2 rounded mt-2"><img src="../assets/images/send_chat.png" style="rotate: 45deg; width: 8.5%; right:4%; bottom:5.5%;position: absolute;  user-select: none;"></button>
                <label for="exportButton" class="ml-2 pr-4 cursor-pointer" title="выгрузить"> <img src="../assets/images/export_chat.png" style="width: 5.4%; bottom: 10%;left: 15%;position: absolute; user-select: none;"></label>
                <div class="create-line" style="height: 20%; width: 0.5%; background-color: #EEDB7B; left: 12%; position: absolute; bottom: 7%; user-select: none;"></div>
                <button id="importButton" class="cursor-pointer" title="загрузить"><img src="../assets/images/import_chat.png" style="width: 5.6%; bottom: 10%;left: 4%;position: absolute;  user-select: none;"></button>
            </div>
        </div> 
        <img src="../assets/images/Filicia_ogiadniechat.gif" style="position: absolute; width: 26%; left: 2%; bottom: 3%;  user-select: none;">
    </div>
</template>
