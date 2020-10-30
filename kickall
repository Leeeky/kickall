if (mb_substr($message,0,8) == '?kickall'){ // Обрезаем сообщение и сравниваем что получилось
    $checkfromiduser = R::findOne('users', 'user_id = ?', [$id]);
    $checkdostyp = $checkfromiduser->dostyp;
    if ($checkdostyp >= 4) { 
        
        $kick_id = mb_substr($message ,9); // еще раз обрезаем и получаем все что написано после /kickall_
        $kick_id = explode("|", mb_substr($kick_id, 3))[0];

        if($kick_id == ""){
            $vk->sendMessage($peer_id, "Вы забыли указать аргумент"); // Проверка указан ли чел,которого кикать
        } elseif(in_array($kick_id, $is_admin)) {
           $vk->sendMessage($peer_id,"Вы не можете исключить системного администратора"); // проверка если кто-то хочет кикнуть овнера бота
        } else {

            $userInfo = $vk->request("users.get", ["user_ids" => $kick_id]); // запрос к вк апи,чтобы получить инфу о человеке
            $first_name = $userInfo[0]['first_name']; // Имя исключаемого пользователя 
            $last_name = $userInfo[0]['last_name']; // Фамилия исключаемого пользователя
            //////////////////////////////////////////////////////////
            $userInfosecond = $vk->request("users.get",["user_ids" => $id,"name_case" => 'gen']);  // Запрос к вк апи,чтобы получить инфу о том,кто кикает, Склоняем (падеж)
            $firstsecond_name = $userInfosecond[0]['first_name']; // имя
            $lastsecond_name = $userInfosecond[0]['last_name']; // фамилия
            /////////////////////////////////////////////////////////
            
            $chat_data = $vk->request('messages.getConversationsById', ['peer_ids' => $peer_id, 'extended' => 0]); // запрос чтобы получить инфу о беседе
            $title = $chat_data['items'][0]['chat_settings']['title']; // получаем тайтл беседы.
            /////////////////////////////////////////////////////////
            $getwarninfo = R::Findone('users','user_id = ?',[$kick_id]);
            $nick = $getwarninfo->nick;
            $isleader = $getwarninfo->isleader;
            $isleaders = $getwarninfo->isleader;
            $idc = implode(" ", $args);
            $clrdostyp = R::Findone('users', 'user_id = ?',[$kick_id]);
           // чистим статистику человека в базе данных
            $validcheck = 1;
            $clrdostyp->dostyp = 1;
            $clrdostyp->isleader = 0;
            $clrdostyp->balls = 0;
            $clrdostyp->reprimand = 0;
            $clrdostyp->warning = 0;
            $clrdostyp->lastupdate = 0;
            $clrdostyp->historywarn = "";
            $clrdostyp->historydellwarn = "";
            $clrdostyp->historyballs = "";
            $clrdostyp->predkurilka = 0;

            $checkserver = $clrdostyp->zakrepby;

            R::store($clrdostyp); 

            if($isleader == 0) {
              $isleader = "Не является лидером фракции";
             }
            if($isleader == 1) {
              $isleader = "Government";
            } 
            if($isleader == 2) {
              $isleader = "ТСР";
            } 
            if($isleader == 3) {
              $isleader = "LSPD";
            } 
            if($isleader == 4) {
              $isleader = "RCSD";
            } 
            if($isleader == 5) {
              $isleader = "SFPD";
            } 
            if($isleader == 6) {
              $isleader = "FBI";
            } 
            if($isleader == 7) {
              $isleader = "SWAT";
            } 
            if($isleader == 8) {
              $isleader = "Army LS";
            } 
            if($isleader == 9) {
              $isleader = "Army SF";
            } 
            if($isleader == 10) {
              $isleader = "LSMC";
            } 
            if($isleader == 11) {
              $isleader = "SFMC";
            } 
            if($isleader == 12) {
              $isleader = "LVMC";
            } 
            if($isleader == 13) {
              $isleader = "R-LS";
            } 
            if($isleader == 14) {
              $isleader = "R-SF";
            } 
            if($isleader == 15) {
              $isleader = "R-LV";
            } 
            if($isleader == 16) {
              $isleader = "Central Bank";
            } 
            if($isleader == 17) {
              $isleader = "Main Licensing Center";
            } 
            if($isleader == 18) {
              $isleader = "Министр Юстиции";
            } 
            if($isleader == 19) {
              $isleader = "Министр Обороны";
            } 
            if($isleader == 20) {
              $isleader = "Министр Здравоохранения";
            } 
            if($isleader == 21) {
              $isleader = "Министр Финансов и Культуры";
            } 
            if($isleader == 22) {
              $isleader = "Warlock MC";
            } 
            if($isleader == 23) {
              $isleader = "La Cosa Nostra";
            } 
            if($isleader == 24) {
              $isleader = "Yakuza";
            } 
            if($isleader == 25) {
              $isleader = "Russian Mafia";
            } 
            if($isleader == 26) {
              $isleader = "Темное братство";
            }
          



            $kickall = 1;
            
            if($checkserver == "") {
              $vk->SendMessage($peer_id,"Пользователь не закреплен за определенным сервером. Произвожу исключения из всех бесед с включенным kickall");
              $wap = R::getAll('SELECT `peer_id` FROM `settings` WHERE `kickall` = ?', [$kickall]); // получаем беседы,где включен кик из всех бесед.
            $vk->SendMessage($peer_id,"Отчет по запросу исключения:\nИнициатор: [id$id|$firstsecond_name $lastsecond_name]");
           foreach($wap as $peer_ik) { // цикл получения бесед
            if($peer_ik['kickall'] == 1) {

            
            $peer_ik['peer_id'];  // уже получаем сам инд.беседы
          }

           foreach($peer_ik as $chat_ik) {
  
           $new_ik = $chat_ik - 2000000000;
           
           
           $checkerror = $vk->request('messages.removeChatUser', array('chat_id' => $new_ik, 'member_id' => $kick_id)); // процедура кика
           $error = $checkerror['error']; // если будет ошибка
           $error = $error['error_code']; // код ошибки,обычно выдает 15 ошибку если не кикает, хз как пофиксить
           
 
           $chat_data = $vk->request('messages.getConversationsById', ['peer_ids' => $chat_ik, 'extended' => 0]);  // title беседы
           $title = $chat_data['items'][0]['chat_settings']['title']; // title besedi


           

           foreach($chat_ik as $peer_i) {
            $da = $vk->request('messages.getConversationMembers',['peer_id' => $peer_i]);
             
             
            
            
         
            
             foreach($da['items'] as $i) {
              foreach($da['profiles'] as $ebannaya) {
                $ebannaya = $ebannaya['id'];
           
              if($i['is_admin'] == 0) {
                $i = $i['is_admin'];
                 
              if($ebannaya == $kick_id) {
                $validationchecksecond = 1;
              }

              } 
         
         
              
         
             }
            }
          }
         


           foreach($chat_ik as $peer_i) {
            $da = $vk->request('messages.getConversationMembers',['peer_id' => $peer_i]);
             
         
             foreach($da['profiles'] as $i) {
              
              if($i['id'] == $kick_id) {
                $validcheck = 1;
              }
        
             }
        
         
          }
        
           if($error == "") {
            
            $vk->SendMessage($peer_id,"✅ID: $chat_ik | Название: $title");
            $vk->sendMessage($chat_ik, "🧍@id$kick_id ($nick) [$isleader]\n✅Удален из беседы по запросу $firstsecond_name $lastsecond_name\nПричина: $idc ");
            
           } elseif($validcheck == 0) {
            
            $vk->SendMessage($peer_id,"❌[Ошибка]: $error | ID: $chat_ik | Название: $title");
           } 
           
           
           
    }
  }
              
            } else {



              // Тоже самое,только кик из бесед,которые закреплены за определенным сервером,группой и т.д. - сначала чекаем за кем закреплен пользователь - потом пробегаемся по беседам с таким сервером и смотрим включен ли кик из всех бесед.
              $wap = R::getAll('SELECT `peer_id` FROM `settings` WHERE `pinserv` = ?', [$checkserver]); 
            $vk->SendMessage($peer_id,"Отчет по запросу исключения:\nИнициатор: [id$id|$firstsecond_name $lastsecond_name]");
           foreach($wap as $peer_ik) {
            if($peer_ik['kickall'] == 1) {

            
            $peer_ik['peer_id']; 
          }

           foreach($peer_ik as $chat_ik) {
  
           $new_ik = $chat_ik - 2000000000;
           
           
           $checkerror = $vk->request('messages.removeChatUser', array('chat_id' => $new_ik, 'member_id' => $kick_id));
           $error = $checkerror['error'];
           $error = $error['error_code'];
           

           $chat_data = $vk->request('messages.getConversationsById', ['peer_ids' => $chat_ik, 'extended' => 0]);
           $title = $chat_data['items'][0]['chat_settings']['title'];




           foreach($chat_ik as $peer_i) {
            $da = $vk->request('messages.getConversationMembers',['peer_id' => $peer_i]);
             
             
            
            
         
            
             foreach($da['items'] as $i) {
              foreach($da['profiles'] as $ebannaya) {
                $ebannaya = $ebannaya['id'];
           
              if($i['is_admin'] == 0) {
                $i = $i['is_admin'];
                 
              if($ebannaya == $kick_id) {
                $validationchecksecond = 1;
              }

              } 
         
         
              
         
             }
            }
          }
         


           foreach($chat_ik as $peer_i) {
            $da = $vk->request('messages.getConversationMembers',['peer_id' => $peer_i]);
             
         
             foreach($da['profiles'] as $i) {
              $validcheck = 0;
              if($i['id'] == $kick_id) {
                $validcheck = 1;
              }
        
             }
        
         
          }
        
           if($error == "") {
            
            $vk->SendMessage($peer_id,"✅ID: $chat_ik | Название: $title");
            $vk->sendMessage($chat_ik, "🧍@id$kick_id ($nick) [$isleader]\n✅Удален из беседы по запросу $firstsecond_name $lastsecond_name\nПричина: $idc ");
            
           } elseif($validcheck == 1) {
            
            $vk->SendMessage($peer_id,"❌[Ошибка]: $error | ID: $chat_ik | Название: $title");
           } 
           
           
           
    }
  }
     }
              
          
            $vk->sendMessage($log, "✅Из беседы: $peer_id \nНазвание: $title\nБыл удален 🧍@id$kick_id ($nick) [$isleader]\nПо запросу $firstsecond_name $lastsecond_name\nПричина: $idc");
            
        }
    } else {
        $vk->sendMessage($peer_id, "Данная команда доступна с 4 уровня доступа. У вас: $checkdostyp");

     }
 }
