

cb.settings_choices = [
    {name:'rule1', type:'str', minLength:1, maxLength:255, label:'Rule #1'},
    {name:'rule2', type:'str', minLength:1, maxLength:255, label:'Rule #2 (optional)', required:false},
    {name:'rule3', type:'str', minLength:1, maxLength:255, label:'Rule #3 (optional)', required:false},
    {name:'rule4', type:'str', minLength:1, maxLength:255, label:'Rule #4 (optional)', required:false},
    {name:'rule5', type:'str', minLength:1, maxLength:255, label:'Rule #5 (optional)', required:false},
    {name:'rule6', type:'str', minLength:1, maxLength:255, label:'Rule #6 (optional)', required:false},
    {name:'rule7', type:'str', minLength:1, maxLength:255, label:'Rule #7 (optional)', required:false},
    {name:'rule8', type:'str', minLength:1, maxLength:255, label:'Rule #8 (optional)', required:false},
    {name:'rule9', type:'str', minLength:1, maxLength:255, label:'Rule #9 (optional)', required:false},
    {name:'rule10', type:'str', minLength:1, maxLength:255, label:'Rule #10 (optional)', required:false},
    {name:'advertisement_wait_time', type:'choice', label:'Notification Time (in minutes)',
        choice1:5, choice2:10, choice3:15, choice4:20, choice5:25, choice6:30, choice7:45, choice8:60,
        defaultValue:15}
];

var meanBroadcasters = ['missilex'];

cb.onEnter(function(user) {
if(meanBroadcasters.indexOf(cb.room_slug) < 0) {
    cb.sendNotice('Welcome, ' + user['user'] + '. Please remember to follow me. Thank you!', user['user'], '#FFFFFF', '', 'bold');
    displayRules(user);
}
});

function displayRules(user) {
    var username = '';
    if(user) username = user['user'];
    var notices = '###### TIP MENU ######';
    for(var i=1; i<=10;i++) {
        if(cb.settings['rule' + i]) notices += '\n'+ i +': ' + cb.settings['rule'+i];
    }
   notices += '\n###### TIP MENU ######';

    cb.sendNotice(notices, username, '#FFFFFF', '#DC5500', 'bold');
    if(!user || user == null) cb.setTimeout(displayRules, cb.settings.advertisement_wait_time * 60000);
}

function init() {
if(meanBroadcasters.indexOf(cb.room_slug) < 0) displayRules();
}

init();
