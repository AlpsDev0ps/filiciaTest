<script>
import { onMounted } from 'vue'
const closeUser = document.getElementById('closeUser')
const closeUserKrasni = document.getElementById('closeUserKrasni')
onMounted(() => {
   closeUser.addEventListener('click', () => {
      console.log(123);
  if (closeUser.value) {
    closeUser.value.hidden = true;
  }
   })
   closeUserKrasni.addEventListener('click', () => {
      console.log(456);
      closeUserKrasni.remove()
   })
})
</script>
<template>
<div class="top"> 
   <text class="logo_text">Фелиция 0.1</text>
   <img class="line_icon" src="../assets/images/line_police.svg">
   <img class="gerb_icon" src="../assets/images/logo_gerb_a.png">
   <img id="button_exit" src="../assets/images/icon_exit.png">
   <button id="statistic">Сводка отчётов</button>
   
  
   <button id="education_UI">Обучить Фелицию</button>
</div>
   
<div class="main">  

   <div id="users_bar"> 
      
      <input type="text" id="search_users" placeholder="Поиск">
      <img src="../assets/images/filter_icon.svg" id="filter_users">
      <input type="button" id="add_user_chat" value="Добавить диалог с Фелицией"> 
      <div id="user_base">
         <img class="icon_user" src="../assets/images/icon_user.png">
         <text class="name_user">Пользователь #1123</text>
         <text class="name_service">ИСОД</text>
         <text class="text_time_online">Последняя активнотсть:</text>
         <text id="time_online">15:12</text>
         <text id="date_online">16.02.24</text>
         <!--добавить статус онлайен -->
         <img class="deleted_user"  id="closeUser" src="../assets/images/icon_delete.svg">
      </div>
      <div class="user_krasni_code">
         <img class="icon_user" src="../assets/images/icon_user.png">
         <text class="name_user">Пользователь #3</text>    
         <img class="deleted_user"  id="closeUserKrasni" src="../assets/images/icon_delete.svg">
         <text class="name_service">ИСОД</text>
         <img class="icon_user_attenson" src="../assets/images/icon_user_attension_a.png">
         <text class="text_time_online">Последняя активнотсть:</text>
         <text id="status_online">online</text>
      </div>
   </div>

    <text id="text_name_user_main">Диалог с<text id="name_user_main"> пользователь №1123</text></text>
    <div class="bar_chat">
      <!--  -->
       <div class="chat"> 
          <div class="message_2">Робот Фелиция поможет в решении ваших вопросов. Я во внимании!</div>
          <div class="message_1">Просьба зарегистрировать обращение на разблокирование учетных записей СЭД.
          </div>
          <div class="message_2">Заявка №11247 по сервису СЭД на разблокировку учётных записей принята, среднее время ожидания...
          </div>
          <div class="message_2">4 часа.</div>
       </div>
       <div class="send_chat"> 
         <textarea id="input_chat"></textarea>
         <img id="export_chat" src="../assets/images/export_chat.png">
         <img id="send_message" src="../assets/images/send_chat.png">
         <img class="felicia_gif" src="../assets/images/Filicia_gif.gif">
       </div>
    </div>
    
</div>

</template>

<style scoped>
* {
    font-family: Roboto Slab;
}
.gerb_icon {
   height: 100px;
   position: absolute;
   left: 1%;
}
.line_icon {
   position: absolute;
   margin-left: 3%;
   margin-top: 3.2%;
 height: 3.5%;
}
.logo_text{
   color: rgb(255, 255, 255);
   position: absolute;
   margin-left: 3%;
   margin-top: 1.5%;
   font-size: 20px;
}
#export_chat{
   width: 2.4%;
   position: absolute;
   bottom: 10%;
   left: 1.5%;
}
#send_message {
   rotate: 45deg;
   width: 3.5%;
   position: absolute;
   bottom: 6%;
   right: 2%;
}
.felicia_gif {
   width: 20%;
   transform: scale(-1, 1) ;
   position: absolute;
   bottom: 0%;
   left: 101%;
}
.send_chat{
   position: absolute;
   bottom: 0%;
   width: 83%;
   height: 19%;
   border-radius: 15px;
   background: white;
}
#input_chat {
   position: absolute;
   bottom: 23%;
   width: 99.5%;
   height: 75%;
   border-radius: 15px;
   border: none;
   outline: none;
   text-align: left;
   resize:none;
   outline:none;
   padding: 15px;
   overflow-x: hidden;
 
}
.bar_chat{ 
   width: 60%;
   height: 80%;
   left: 36%;
   margin-top: 7%;
   position: relative;
}
#filter_users {
   width: 3.5%;
   height: 20px;
   float: right;
   margin-top: 2.5%;
   margin-right: 2%;
}
#search_users{
   float: right;
   margin-top: 2.5%;
   margin-right: 5%;
   border: none;
   border-radius: 5px;
   background: #F9F9F9;
   color: #888888;
   user-select: none;
   border: none;
   outline: none;
}
#button_exit{
   height: 20px;
   float: right;
   margin: 25px;
   color: #D9D9D9;
   right: 1%;
  
}
#education_UI{
   float: right;
   margin-top: 22px;
   margin-right: 40px;
   border:none;
   border-radius: 8px;
   height: 27px;
   background: #e3e9ff;
   color: #1C356E;
}
#statistic{
   float: right;
   margin-top: 22px;
   margin-right: 100px;
   border-radius: 5px;
   height: 27px;
   border:none;
   border-radius: 8px;
   background: #e3e9ff;
   color: #1C356E;
}

.message_2 {
   font-size: 80%;
   background-color: #EFF2FF;
   text-wrap: wrap;
   text-align: left;
   margin-left: 50%;
   margin-right: 15%;
   padding: 15px;
   border-radius: 15px;
   overflow-wrap: normal;
   max-width: 45%;
   margin-top: 2%;
   color: #2B48B0
}
.message_1 {
	
   font-size: 80%;
   background-color: #C9D4EA;
   color: #213788;
   text-wrap: wrap;
   text-align: left;
   float: left;
   padding: 15px;
   border-radius: 15px;
   overflow-wrap: normal;
   max-width: 45%;
   margin-top: 3%; 
}
.chat{
   position: absolute;
   flex-direction: column;
   display: flex;
   overflow-y: auto;
   width: 100%;
   height: 80%;
   
   
}
#text_name_user_main {
   top: 12%;
   margin-left: 60%;
   position: absolute;
   font-size: 90%;
   color: #1C356E;
}
.icon_user_attenson {
   float: left;
   margin-left: 4%;
   width: 5%;
   margin-top: 1.5%;
}
.user_krasni_code {
   width: 90%;      
   border-radius: 15px;
   background-color: #FFC2C2;
   height: 70px;                   /* окно маленькое на маленьких экранах */
   margin-top: 3%;
   margin-left: 5%;
   position: absolute;
   border-width: 1px;
   color: #1C356E;
}
#status_online {
   font-size: 80%;
    position: absolute;
   left: 85%;
   bottom: 10%;
   font-size: 80%;
   color: #0DA600;
}
.deleted_user {
   width: 6%;
   right: 12px;
  float: right;
  margin: 1%;
  color: #0DA600;
}
#date_online {
    font-size: 80%;
    position: absolute;
   left: 85%;
   bottom: 10%;
   font-size: 80%;
}
#time_online {
    font-size: 80%;
    position: absolute;
   left: 70%;
   bottom: 10%;
   font-size: 80%;
}
.text_time_online {
   position: absolute;
   left: 16%;
   bottom: 10%;
   font-size: 80%;
}
.name_service {
  font-style:oblique;
  margin-top: 5px;
  max-width: 50%;
  float: left;
  font-size: 80%;
  margin-left: 2%;
}
.name_user {
  margin-top: 5px;
  float: left;
  font-size: 80%;
  position: relative;
}
.icon_user {
   /* цвет иконки */
   float: left;
   width: 12%;
   margin: 2%;
}
#user_base {
   width: 90%;      
   border-radius: 15px;
   background-color: #FFFFFF;
   height: 70px;                   /* окно маленькое на маленьких экранах */
   margin-top: 3%;
   margin-left: 5%;
   position: relative;
   border-width: 1px;
   color: #1C356E;
   
}
#add_user_chat {
   width: 90%;      
   border-radius: 15px;
   background-color: #EEEEEE;
   height: 70px;                   /* окно маленькое на маленьких экранах */
   margin-top: 2%;
   margin-left: 5%;
   position: absolute;
   border-width: 1px;
   color: #1C356E;
   position: relative;
   font-size: 80%;
}
.main {
   position: absolute;
   width: 100%;
   height: 100%;
}
.top {
    width: 100%;
    height: 70px;
    background-color: #1C356E;
    position: absolute;
    top: 0%;
    left: 0%;
}
#users_bar {
    background-color: #D9D9D9;
    position: absolute;
    width: 30%;
    height: 83%;
    border-radius: 2%;
    margin-top: 6%;
    margin-left: 1%;
    overflow-y: auto;
}
.gerb_icon {
   height: 100%;
   margin-left: 45%;
   user-select: none;
}
</style>