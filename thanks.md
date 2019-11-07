---
layout: page
title: Contributors
permalink: /thanks
icon: people
---

<h1>Thanks</h1>

Constellation is a community project and is very thankful for the community contributions it receives.

Check out the contributors to [Amadeus](https://github.com/constellation-rs/amadeus/graphs/contributors) and [Constellation](https://github.com/constellation-rs/constellation/graphs/contributors) on GitHub.

<p id="contributors-count"></p>

<table id="contributors"></table>

<style>
.addition {
  color: #28a745;
}
.deletion {
  color: #cb2431;
}
</style>
<script>
'use strict';
(function() {
  // https://developer.github.com/v3/repos/statistics/

  let count = document.getElementById('contributors-count');
  let table = document.getElementById('contributors');

  function request(url, callback) {
    var req = new XMLHttpRequest();
    req.open('GET', url);
    req.addEventListener('readystatechange', function() {
      if (req.readyState === 4) {
        if (req.status === 200) {
          callback(req.responseText, null);
        } else if (req.status === 202 || (500 <= req.status && req.status <= 599)) {
          setTimeout(function() {
            request(url, callback);
          }, 2000);
        } else {
          callback(null, req);
        }
      }
    });
    req.send();
  }

  function requestJSON(url, callback) {
    request(url, function(response, err) {
      callback(JSON.parse(response), err);
    });
  }

  let repos = ['constellation-rs/amadeus', 'constellation-rs/constellation', 'alecmocatta/palaver', 'alecmocatta/serde_closure', 'alecmocatta/relative', 'alecmocatta/cargo-print', 'alecmocatta/cap', 'alecmocatta/serde_traitobject', 'alecmocatta/build_id', 'alecmocatta/metatype', 'alecmocatta/replace_with', 'alecmocatta/streaming_algorithms', 'alecmocatta/reqwest_resume', 'alecmocatta/notifier', 'alecmocatta/tcp_typed', 'alecmocatta/socketstat', 'alecmocatta/serde_pipe', 'alecmocatta/sum', 'alecmocatta/azure-pipeline-templates'];

  var awaiting = 0;
  var results = [];

  let success = function(committers, err) {
    if (committers) {
      results.push(committers);
    }
    if (err) {
      console.log(err);
    }
    awaiting -= 1;
    if (awaiting === 0) {
      done(results);
    }
  };
  for (var i = 0; i < repos.length; i++) {
    let repo = repos[i];
    let url = 'https://api.github.com/repos/' + repo + '/stats/contributors';
    awaiting += 1;
    requestJSON(url, success);
  }

  function done(committerss) {
    let map = {};
    for (var x = 0; x < committerss.length; x++) {
      let committers = committerss[x];
      for (var i = 0; i < committers.length; i++) {
        let committer = committers[i];
        if (committer['author']['login'] == 'dependabot-bot') {
          continue;
        }
        var record;
        if (!(committer['author']['login'] in map)) {
          record = [0, 0, 0];
          map[committer['author']['login']] = record;
        } else {
          record = map[committer['author']['login']];
        }
        record[0] += committer['total'];
        let weeks = committer['weeks'];
        var additions = 0;
        var deletions = 0;
        for (var j = 0; j < weeks.length; j++) {
          let week = weeks[j];
          additions += week['a'];
          deletions += week['d'];
        }
        record[1] += additions;
        record[2] += deletions;
      }
    }
    let vec = [];
    for (var name in map) {
      let stats = map[name];
      vec.push([name, stats[0], stats[1], stats[2]]);
    }
    vec.sort(function(a, b) {
      var cmp = b[1] - a[1];
      if (cmp == 0) {
        cmp = (b[2] + b[3]) - (a[2] + a[3]);
      }
      if (cmp == 0) {
        cmp = Math.max(b[2], b[3]) - Math.max(a[2], a[3]);
      }
      if (cmp == 0) {
        cmp = b[2] - a[2];
      }
      return cmp;
    });

    count.appendChild(document.createTextNode('We have had ' + vec.length + ' individuals contribute to Constellation and its supporting crates so far. Thank you so much!'));

    for (var i = 0; i < vec.length; i++) {
      let contributor = vec[i];
      var tr = document.createElement('tr');
      var td = document.createElement('td');
      let link = document.createElement('a');
      link.href = 'https://github.com/' + contributor[0];
      link.appendChild(document.createTextNode(contributor[0]));
      td.appendChild(link);
      tr.appendChild(td);
      var td = document.createElement('td');
      td.appendChild(document.createTextNode(contributor[1].toLocaleString() + ' commits '));
      let addition = document.createElement('span');
      addition.className = 'addition';
      addition.appendChild(document.createTextNode(contributor[2].toLocaleString() + ' ++'));
      td.appendChild(addition);
      td.appendChild(document.createTextNode(' '));
      let deletion = document.createElement('span');
      deletion.className = 'deletion';
      deletion.appendChild(document.createTextNode(contributor[3].toLocaleString() + ' --'));
      td.appendChild(deletion);
      tr.appendChild(td);
      table.appendChild(tr);
    }
  }
})()
</script>
