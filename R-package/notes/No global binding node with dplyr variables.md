
## Node

❯ checking R code for possible problems ... NOTE
  find_outlier_eval_box: no visible binding for global variable
    ‘best_query’
  find_outlier_eval_box: no visible binding for global variable
    ‘ViralRefSeq_E’
  generate_run_bar_table: no visible binding for global variable
    ‘best_query’
  preprocess_runs_bar: no visible binding for global variable
    ‘best_query’
  preprocess_runs_bar: no visible binding for global variable
    ‘unique_SRA_run’


## Solution: use .data from rlang

#' @title vh_refeval_iden_boxplot: Create a formatted table using the gt package
#'
#' @description This function takes summary statistics and creates a formatted table using
#' the gt package.
#'
#' @param summary_stats A data frame containing summary statistics
#'
#' @return A formatted gt table
#'
#' @details This function is for internal use within the package.
#' It formats summary statistics into a table
#' using the gt package for further evaluation.
#'
#' @seealso \code{\link{vh_refeval_iden_boxplot}}
#' @importFrom gt gt fmt_number
#' @importFrom rlang .data
#' @keywords internal
creat_table_eval_box <- function(summary_stats){

  # Create gt table
  gt_table <- summary_stats %>%
    gt()%>%
    fmt_number(
      columns = !.data$below_threshold,
      decimals = 2
    )

  gt_table

  return(gt_table)
}

Here below_threshold caused the node

Source: https://forum.posit.co/t/how-to-solve-no-visible-binding-for-global-variable-note/28887/2