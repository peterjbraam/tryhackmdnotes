# Todo / Task management systems. - taspaper

# Taskpaper Editor Requirements

## Must have

- archive complete items saving project and date, removing other tags (drafts 5:yes, editorial: yes, TaskPaper: yes)
- Project format is exportable to markdown (editorial:yes)
- Narrow down on a project (drafts 5: yes, editorial: yes)
- Narrow down on a tag (**drafts 5: not really**, editorial: yes)
- Copy or Move from Reminders (drafts: yes, editorial: yes)
- Export to reminders (TaskPaper: yes

## Good to have
- Collapse / Folding (TaskPaper: yes, **drafts 5:no**, editorial: yes)
- Create a reminder for some task (drafts:yes, editorial: yes)
- Move blocks “arrange” plugin (editorial: yes, drafts: yes)

## Drafts 5 task paper references

[taskpaper drafts actions - drang](https://leancrew.com/all-this/2018/05/taskpaper-actions-for-drafts-5/)
[taskpaper drafts improvement - drang](https://leancrew.com/all-this/2018/05/a-taskpaper-drafts-improvement/)
[actions collected for these two](https://actions.getdrafts.com/g/1Hp)
[jump to TP project](https://actions.getdrafts.com/a/1Fy)
[using reminders with drafts 5](https://forums.getdrafts.com/t/using-reminders-with-drafts/81)


## Editorial iOS taskpaper references

[set reminders](http://www.editorial-workflows.com/workflow/5314928277716992/3OEDkjV7EeQ) - sets reminders based on a tag
[dr drang taspaper in editorial](http://dfay.fastmail.fm/et/)
[syn reminders py](https://github.com/andsx/editorial-reminders/blob/master/sync_reminders.py) - somewhat unfinished script that syncs reminders with projects in a TP file
[editorial list reminders](http://www.editorial-workflows.com/workflow/5012964226629632/_BycaAdg3Vg)- doesn't mark listed ones complete; I hacked that into the iPad version

# TaskPaper dev - archive by project

From Jesse Grosjean

Archive by project:
```
archiveDone = (editor) ->
  outline = editor.outline
  selection = editor.selection
  startItem = selection.startItem
  endItem = selection.endItem
  archive = outline.evaluateItemPath("//@text = Archive:")[0]
  doneItems = Item.getCommonAncestors(outline.evaluateItemPath("//@done except //@text = Archive://@done"))
  removeExtraTags = Birch.preferences.get('BRemoveExtraTagsWhenArchivingDone')
  addProjectTag = Birch.preferences.get('BIncludeProjectWhenArchivingDone')

  outline.groupUndoAndChanges ->
    unless archive
      outline.root.appendChildren(archive = outline.createItem('Archive:'))
    for each in doneItems
      if removeExtraTags
        for eachName in each.attributeNames
          if eachName.indexOf('data-') is 0 and eachName isnt 'data-type' and eachName isnt 'data-done'
            each.removeAttribute(eachName)
      if addProjectTag
        if projects = (eachProject.bodyContentString for eachProject in outline.evaluateItemPath('ancestor::@type=project', each)).join(' / ')
          each.setAttribute('data-project', projects)
      if (each is startItem or each.contains(startItem)) or (each is endItem or each.contains(endItem))
        if previousItem = editor.getPreviousDisplayedItem(startItem)
          selection = startItem: previousItem, startOffset: -1
        else
          selection = start: 0
    archive.insertChildrenBefore(doneItems, archive.firstChild)
  editor.moveSelectionToItems(selection)
```

# Tasks - Alfred RTM plugin

Tasks: a possible task is found in email, during a call, while having a thought. 

1. **Capture** the task in the Worflowy INBOX, or in RTM work or RTM personal
2. **Alfred:** "r Task !1 \^tomorrow \*after one week \
3. **Backups:** occasionally backup task logs. Is barely happening.
4. **Tools:** seem among the least satisfactory

