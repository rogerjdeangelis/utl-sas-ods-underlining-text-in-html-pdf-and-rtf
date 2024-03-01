# utl-sas-ods-underlining-text-in-html-pdf-and-rtf
sas ods underlining text in html pdf and rtf 
    %let pgm=utl-sas-ods-underlining-text-in-html-pdf-and-rtf;

    sas ods underlining text in html pdf and rtf

      SOLUTIONS

         1 proc report pdf rtf html
         2 ods put rtf
         3 ods table pdf html

    github
    https://tinyurl.com/3vhf33kf
    https://github.com/rogerjdeangelis/utl-sas-ods-underlining-text-in-html-pdf-and-rtf

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /**************************************************************************************************************************/
    /*                                            |                                         |                                 */
    /*            INPUT                           | 1 SAS PDF RTF and HTML                  |      OUTPUT                     */
    /*            =====                           | ======================                  |      ======                     */
    /* WORK.VARVAL total obs=2 01MAR2024:12:52:46 |  ods pdf file="d:/pdf/varval.pdf";      | Mailling Address                */
    /*                                            |  proc report data=varval                |                                 */
    /* Obs     VAR      VAL                       |    style(report)={rules=none};          | Roger :  5349 N Fort Yuma Trail */
    /*                                            |   title "Mailling Address";             |          ---------------------- */
    /*  1     Roger  :  5349 N Fort Yuma Trail    |   cols var val;                         | State :  AZ 85750*              */
    /*  2     State  :  AZ 85750                  |   define var / display " ";             |          --------               */
    /*                                            |   define val /display " "               |                                 */
    /*                                            |      style={textdecoration=underline};  | *Cannot show udnerline           */
    /*                                            |  run;quit;                              | But is underlined in pdf file   */
    /*                                            |  ods pdf close;                         |                                 */
    /*--------------------------------------------+-----------------------------------------+---------------------------------*/
    /*                                            |                                         |                                 */
    /*                                            | 2 ODS PUT RTF                           |                                 */
    /*                                            | =============                           |                                 */
    /*                                            |  %let name    =Roger;                   |                                 */
    /*                                            |  %let address =5349 N Fort Yuma Trail;  |                                 */
    /*                                            |  %let city    =Tucson;                  |                                 */
    /*                                            |  %let state   =AZ 85750;                |                                 */
    /*                                            |                                         |                                 */
    /*                                            |  * you may need to resize               |                                 */
    /*                                            |     because of wrapping;                |                                 */
    /*                                            |  options validvarname=any;              |                                 */
    /*                                            |  ods escapechar='^';                    |                                 */
    /*                                            |  ods rtf file='d:/rtf/varvalrtf.rtf';   |                                 */
    /*                                            |  data _null_;                           |                                 */
    /*                                            |  length 'Mailling Address'n $100;       |                                 */
    /*                                            |  file print ods;                        |                                 */
    /*                                            |  'Mailling Address'n=                   |                                 */
    /*                                            |    "^R/RTF'\ul0 &name \ul &address'";   |                                 */
    /*                                            |  put _ods_ ;                            |                                 */
    /*                                            |  'Mailling Address'n=                   |                                 */
    /*                                            |   "^R/RTF'\ul0 &city \ul &state'";      |                                 */
    /*                                            |  put _ods_ ;                            |                                 */
    /*                                            |  run;                                   |                                 */
    /*                                            |  ods rtf close;                         |                                 */
    /*--------------------------------------------+-----------------------------------------+---------------------------------*/
    /*                                            |                                         |                                 */
    /*                                            | 3 ODS TABLE PDF HTML                    |                                 */
    /*                                            | ====================                    |                                 */
    /*                                            |  options nodate nonumber;               |                                 */
    /*                                            |  ods html path="d:/htm"                 |                                 */
    /*                                            |    file="varvalhtm.html";               |                                 */
    /*                                            |  ods pdf file="d:/pdf/varvalpdf.pdf";   |                                 */
    /*                                            |                                         |                                 */
    /*                                            |  title "Mailing Address";               |                                 */
    /*                                            |                                         |                                 */
    /*                                            |  data _null_;                           |                                 */
    /*                                            |                                         |                                 */
    /*                                            |   set varval end=eof;                   |                                 */
    /*                                            |                                         |                                 */
    /*                                            |   if _n_=1 then do;                     |                                 */
    /*                                            |   dcl odsout obj();                     |                                 */
    /*                                            |    obj.table_start(                     |                                 */
    /*                                            |        label: "Mailing Address" );      |                                 */
    /*                                            |   end;                                  |                                 */
    /*                                            |                                         |                                 */
    /*                                            |   obj.row_start();                      |                                 */
    /*                                            |   obj.format_cell(data: VAR);           |                                 */
    /*                                            |   obj.format_cell(data: VAL,            |                                 */
    /*                                            |   style_attr:"textdecoration=underline" |                                 */
    /*                                            |   obj.row_end();                        |                                 */
    /*                                            |   if eof then do;                       |                                 */
    /*                                            |   obj.table_end();                      |                                 */
    /*                                            |   end;                                  |                                 */
    /*                                            |    run;                                 |                                 */
    /*                                            |                                         |                                 */
    /*                                            |    ods _all_ close;                     |                                 */
    /*                                            |    ods html;                            |                                 */
    /*                                            |                                         |                                 */
    /*                                            |   run;quit;                             |                                 */
    /*                                            |                                         |                                 */
    /***************************************************************************************|**********************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    data varval;
    length var val $40;
    var="Roger  :" ;val="5349 N Fort Yuma Trail";output;
    var="Tucson :"; val="AZ 85750"             ;output;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* data varval;                                                                                                           */
    /* length var val $40;                                                                                                    */
    /* var="Roger  :" ;val="5349 N Fort Yuma Trail";output;                                                                   */
    /* var="State  :"; val="AZ 85750"              ;output;                                                                   */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*                                                    _               _  __        _    __   _     _             _
    / |  _ __  _ __ ___   ___   _ __ ___ _ __   ___  _ __| |_   _ __   __| |/ _|  _ __| |_ / _| | |__ | |_ _ __ ___ | |
    | | | `_ \| `__/ _ \ / __| | `__/ _ \ `_ \ / _ \| `__| __| | `_ \ / _` | |_  | `__| __| |_  | `_ \| __| `_ ` _ \| |
    | | | |_) | | | (_) | (__  | | |  __/ |_) | (_) | |  | |_  | |_) | (_| |  _| | |  | |_|  _| | | | | |_| | | | | | |
    |_| | .__/|_|  \___/ \___| |_|  \___| .__/ \___/|_|   \__| | .__/ \__,_|_|   |_|   \__|_|   |_| |_|\__|_| |_| |_|_|
        |_|                             |_|                    |_|
    */

    ods pdf file="d:/pdf/1_varval.pdf";
    proc report data=varval
      style(report)={rules=none};
     title "Mailling Address";
     cols var val;
     define var / display " ";
     define val /display " "
        style={textdecoration=underline};
    run;quit;
    ods pdf close;

    ods rtf file="d:/rtf/1_varval.rtf";
    proc report data=varval
      style(report)={rules=none};
     title "Mailling Address";
     cols var val;
     define var / display " ";
     define val /display " "
        style={textdecoration=underline};
    run;quit;
    ods rtf close;

    ods html path="d:/htm"  body="1_varval.htm" style=minimal;
    proc report data=varval
      style(report)={rules=none};
     title "Mailling Address";
     cols var val;
     define var / display " ";
     define val /display " "
        style={textdecoration=underline};
    run;quit;
    ods html close;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* Mailling Address                                                                                                       */
    /*                                                                                                                        */
    /* Roger :  5349 N Fort Yuma Trail                                                                                        */
    /*          ----------------------                                                                                        */
    /* State :  AZ 85750                                                                                                      */
    /*          --------                                                                                                      */
    /**************************************************************************************************************************/

    /*___              _                   _          _    __
    |___ \    ___   __| |___   _ __  _   _| |_   _ __| |_ / _|
      __) |  / _ \ / _` / __| | `_ \| | | | __| | `__| __| |_
     / __/  | (_) | (_| \__ \ | |_) | |_| | |_  | |  | |_|  _|
    |_____|  \___/ \__,_|___/ | .__/ \__,_|\__| |_|   \__|_|
                              |_|
    */

    data varval;
    length var val $40;
    var="Roger  :" ;val="5349 N Fort Yuma Trail";output;
    var="Tucson :"; val="AZ 85750"             ;output;
    run;quit;

    %let name    =Roger;
    %let address =5349 N Fort Yuma Trail;
    %let city    =Tucson;
    %let state   =AZ 85750;

    * you may need to resize
       because of wrapping;
    options validvarname=any;
    ods escapechar='^';
    ods rtf file='d:/rtf/2_varvalrtf.rtf';
    data _null_;
    length 'Mailling Address'n $100;
    file print ods;
    'Mailling Address'n=
      "^R/RTF'\ul0 &name \ul &address'";
    put _ods_ ;
    'Mailling Address'n=
     "^R/RTF'\ul0 &city \ul &state'";
    put _ods_ ;
    run;
    ods rtf close;

    /*____             _       _        _     _                  _  __   _     _             _
    |___ /    ___   __| |___  | |_ __ _| |__ | | ___   _ __   __| |/ _| | |__ | |_ _ __ ___ | |
      |_ \   / _ \ / _` / __| | __/ _` | `_ \| |/ _ \ | `_ \ / _` | |_  | `_ \| __| `_ ` _ \| |
     ___) | | (_) | (_| \__ \ | || (_| | |_) | |  __/ | |_) | (_| |  _| | | | | |_| | | | | | |
    |____/   \___/ \__,_|___/  \__\__,_|_.__/|_|\___| | .__/ \__,_|_|   |_| |_|\__|_| |_| |_|_|
                                                      |_|
    */

    options nodate nonumber;
    ods html path="d:/pdf"
      file="3_varvalhtm.html";
    ods pdf file="d:/pdf/3_varvalpdf.pdf";

    title "Mailing Address";

    data _null_;

      set varval end=eof;

      if _n_=1 then do;
      dcl odsout obj();
       obj.table_start(
           label: "Mailing Address" );
      end;

      obj.row_start();
      obj.format_cell(data: VAR);
      obj.format_cell(data: VAL,
       style_attr: "textdecoration=underline");
      obj.row_end();
      if eof then do;
      obj.table_end();
      end;
      run;

      ods _all_ close;
      ods html;

    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* Mailling Address                                                                                                       */
    /*                                                                                                                        */
    /* Roger :  5349 N Fort Yuma Trail                                                                                        */
    /*          ----------------------                                                                                        */
    /* State :  AZ 85750                                                                                                      */
    /*          --------                                                                                                      */
    /**************************************************************************************************************************/

