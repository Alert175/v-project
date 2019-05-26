<template>
    <div class="timer">
        осталось дней: {{theTime.days}}<br>
        осталось часов: {{theTime.hours}}<br>
        осталось минут: {{theTime.minutes}}<br>
        осталось секунд: {{theTime.seconds}}
    </div>
</template>
<script>
export default {
    data() {
        return{
            deadline: 'May 27, 2019 23:59:59',
            days: 'HI',
            hours: 'TH',
            minutes: 'ER',
            seconds: 'E!',
            expired: false
        }
    },
    computed: {
        theTime(){
        var ctx = this;
        
        // Цикл обратного отсчета
        var x = setInterval(function(){
        
            //Разница между двумя датами
            var countDownDate = new Date(ctx.deadline).getTime(),
            now = new Date().getTime(),
            diff = countDownDate - now,
            
            // Преобразование времени в дни, часы, минуты и секунды
            tdays = Math.floor(diff / (1000 * 60 * 60 * 24)),
            thours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)),
            tminutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60)),
            tseconds = Math.floor((diff % (1000 * 60)) / 1000);
            
            // Отображать две цифры
            ctx.days = (tdays < 10) ? '0' + tdays : tdays;
            ctx.hours = (thours < 10) ? '0' + thours : thours;
            ctx.minutes = (tminutes < 10) ? '0' + tminutes : tminutes;
            ctx.seconds = (tseconds < 10) ? '0' + tseconds : tseconds;
            
            // Проверка истечения времени
            if(diff < 0){
                clearInterval(x);
                ctx.expired = true;
                }
            }, 1000);
        
        // Возвращение данных
        return {
            days: ctx.days,
            hours: ctx.hours,
            minutes: ctx.minutes,
            seconds: ctx.seconds
            };
        }
    }
}
</script>