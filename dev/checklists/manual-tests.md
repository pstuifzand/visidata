# Functionality to test manual
1. cmdlog + replay
    - logging of options
    - logging of rows and columns
    - if empty sheet, row or column on cmdlog, executes command on current sheet, row, column
    - pause, continue, abort
    - test batch mode
        - bin/vd -b -p tests/append.vd
        - bin/vd -p tests/append.vd -b
2. piping data into visidata
4. longname-exec
5. syscopy
6. plots and image-loaders (like png)
    - relationship between plots and mice
8. .visidatarc
    - numerical, boolean and string option
    - sheet-specific and global
    - motd_url
9. using the pandas loader
    - select
    - edit
    - frequency table
10. large dataset (311)
11. multiline scrolling tests
    - test case 1
        - use vgit
        - main status sheet is 1 line per row, scroll down manually to the bottom
        - and past, ensure it scrolls well
        - and then scroll to the top, and make sure it scrolls back
     - test case 2
        - start a few down from the top
        - Ctrl+F
        - make sure the cursor stays relatively positioned
        - Ctrl+F and Ctrl+B should be reserves, at least in the middle of the sheet
        - and then all the way to the bottom; j does nothing
        - gj always puts the cursor on the bottom row
     - test case 3
        - Shift+L for log, same tests
12. Options
    - local + global options should be set appropriately
        - bin/vd -f tsv sample_data/sample.tsv -f csv sample_data/benchmark.csv
        - bin/vd sample_data/y77d-th95.json.gz -f txt
    - the order in which options should be applied is
        - native_options -> cli_options for config/visidata_dir/imports -> plugin_imports -> visidatarc -> rest_of_cli
        - check that cli overwrites visidatarc
        - check that --config selects which visidatarc to load
        - check that visidatarc can set plugin options
    - -w and others should be set "globally" (work without -g option)
    - bin/vd -f xlsx sample_data/sample-sales-reps.xlsx -f json sample_data/y77d-th95.json.gz
        - the xlsx sheet should have filetype 'xlsx'
    - bin/vd sample_data/sample-sales-reps.xlsx -n -f xlsx
        - `o` another file
        - check that it loads
        - check that it does not show 'xlsx' on its sheet-specific options
13. Filetype
    - visidata should be able to detect filetype from extension
        - bin/vd sample_data/benchmark.csv
    - -f should apply to inner file for zipped filetypes
        - bin/vd -f txt sample_data/y77d-th95.json.gz
14. Testing the starting position syntax
    - `bin/vd +:sample-salesv4:: sample_data/sample-sales-reps.xlsx`
15. Test loading url
16. Split window
    - make sure that if you exit split window, all the sheets from both panes can be accessible on the resulting stack
    - test 1
        - open 2 files
        - Z
        - first window should be active
        - Tab between
        - close top one, then redo and test closing bottom one
            - bug?
                - does not fullsize
            - when top pane is quit, bottom pane is moved to the top
    - test 2
        - open 2 files
        - Z
        - open columns sheet in one
        - Z
        - inspect sheet stack
            - columns sheet should remain where it is, and the source sheet below gets moved to the top of the other window
        - redo with opening the columns sheet on the other
            - bug
                - when Shift+Z is done on bottom pane, its second sheet becomes the second sheet of the top stack, isntead of the first sheet of the top stack
        - test 3
            - Shift+Z with only one file
            - Shift+Z with two panes, each pane's stack only has one file
    - gZ
        - test both panes
        - move around, should be no flickering
        - press Z again
        - test both panes
    - zZ
        - should change window size, without changing anything else
        - test for both panes
        - test negative and positive
            - bug?
                - negative switches the windows they belong to
    - gTab
        - should window swap
        - test both panes
            - bug?
                - if the second window is a smaller size, should it orient around the cursor position
    - using cursor in active pane
        - test both panes
17. Anything new in this release (should it have its own automated test?)
18. `edit-cell` and then `Ctrl+O` to launch editor.
